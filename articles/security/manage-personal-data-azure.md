---
title: "在 Microsoft Azure 中的個人資料 aaaManage |Microsoft 文件"
description: "指引 toocorrect，如何更新、 刪除及匯出 Azure Active Directory 和 Azure SQL Database 中的個人資料"
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.openlocfilehash: 032f70d32377cb9395cb2c35c27dad05001537c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-personal-data-in-microsoft-azure"></a><span data-ttu-id="37e24-103">在 Microsoft Azure 中管理個人資料</span><span class="sxs-lookup"><span data-stu-id="37e24-103">Manage personal data in Microsoft Azure</span></span>

<span data-ttu-id="37e24-104">本文提供指引 toocorrect，如何更新、 刪除及匯出 Azure Active Directory 和 Azure SQL Database 中的個人資料。</span><span class="sxs-lookup"><span data-stu-id="37e24-104">This article provides guidance on how toocorrect, update, delete, and export personal data in Azure Active Directory and Azure SQL Database.</span></span>

## <a name="scenario"></a><span data-ttu-id="37e24-105">案例</span><span class="sxs-lookup"><span data-stu-id="37e24-105">Scenario</span></span>

<span data-ttu-id="37e24-106">Dublin 公司提供高階目的地結婚愛爾蘭及本機和國際客戶基底的 hello world 購買一次。</span><span class="sxs-lookup"><span data-stu-id="37e24-106">A Dublin-based company provides one-stop shopping for high end destination weddings in Ireland and around hello world for both a local and international customer base.</span></span> <span data-ttu-id="37e24-107">它們有辦公室、 客戶、 員工和廠商各地 hello world toofully 服務 hello 管道時所提供。</span><span class="sxs-lookup"><span data-stu-id="37e24-107">They have offices, customers, employees, and vendors located around hello world toofully service hello venues they offer.</span></span>

<span data-ttu-id="37e24-108">在許多其他項目，hello 公司會追蹤的與會者包含食物的過敏情況和飲食喜好設定。</span><span class="sxs-lookup"><span data-stu-id="37e24-108">Among many other items, hello company keeps track of RSVPs that include food allergies and dietary preferences.</span></span> <span data-ttu-id="37e24-109">告別來賓可以註冊的各種活動，例如有時騎馬 riding，瀏覽，船了，以此類推，與甚至彼此互動管理中心的 web 網頁上 hello 月乃至 toohello 事件期間。</span><span class="sxs-lookup"><span data-stu-id="37e24-109">Wedding guests can register for various activities such as horseback riding, surfing, boat rides, etc., and even interact with one another on a central web page during hello months leading up toohello event.</span></span> <span data-ttu-id="37e24-110">hello 公司會從員工、 廠商、 客戶和場遊客收集個人資訊。</span><span class="sxs-lookup"><span data-stu-id="37e24-110">hello company collects personal information from employees, vendors, customers, and wedding guests.</span></span> <span data-ttu-id="37e24-111">因為 hello 國際性質 hello 商務 hello 公司必須符合規定的多個層級。</span><span class="sxs-lookup"><span data-stu-id="37e24-111">Because of hello international nature of hello business hello company must comply with multiple levels of regulation.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="37e24-112">問題陳述</span><span class="sxs-lookup"><span data-stu-id="37e24-112">Problem statement</span></span>

- <span data-ttu-id="37e24-113">資料的系統管理員必須能夠 toocorrect 不正確個人資訊及更新未完成或變更個人資訊。</span><span class="sxs-lookup"><span data-stu-id="37e24-113">Data admins must be able toocorrect inaccurate personal information and update incomplete or changing personal information.</span></span>

- <span data-ttu-id="37e24-114">資料的系統管理員需要必須能夠 toodelete 個人 hello 要求資料主體資訊。</span><span class="sxs-lookup"><span data-stu-id="37e24-114">Data admins need must be able toodelete personal information upon hello request of a data subject.</span></span>

- <span data-ttu-id="37e24-115">資料的系統管理員需要 tooexport 資料，並提供它 tooa 資料主旨常見且結構化的格式，依據他或她的要求。</span><span class="sxs-lookup"><span data-stu-id="37e24-115">Data admins need tooexport data and provide it tooa data subject in a common, structured format upon his or her request.</span></span>

## <a name="company-goals"></a><span data-ttu-id="37e24-116">公司目標</span><span class="sxs-lookup"><span data-stu-id="37e24-116">Company goals</span></span>

- <span data-ttu-id="37e24-117">必須在 Azure Active Directory 與 Azure SQL Database 中更正或更新不正確或不完整的客戶、婚禮賓客、員工及合作廠商的個人資訊。</span><span class="sxs-lookup"><span data-stu-id="37e24-117">Inaccurate or incomplete customer, wedding guest, employee, and vendor personal information must be corrected or updated in Azure Active Directory and Azure SQL Database.</span></span>

- <span data-ttu-id="37e24-118">依據資料主旨 hello 要求，必須在 Azure Active Directory 和 Azure SQL Database 中刪除的個人資訊。</span><span class="sxs-lookup"><span data-stu-id="37e24-118">Personal information must be deleted in Azure Active Directory and Azure SQL Database upon hello request of a data subject.</span></span>

- <span data-ttu-id="37e24-119">必須依據 hello 資料主體要求以通用的結構化格式匯出個人資料。</span><span class="sxs-lookup"><span data-stu-id="37e24-119">Personal data must be exported in a common, structured format upon hello request of a data subject.</span></span>

## <a name="solutions"></a><span data-ttu-id="37e24-120">解決方案</span><span class="sxs-lookup"><span data-stu-id="37e24-120">Solutions</span></span>

### <a name="azure-active-directory-rectifycorrect-inaccurate-or-incomplete-personal-data-and-erasedelete-personal-datauser-profiles"></a><span data-ttu-id="37e24-121">Azure Active Directory：改正/更正不正確或不完整的個人資料，並清除/刪除個人資料/使用者設定檔</span><span class="sxs-lookup"><span data-stu-id="37e24-121">Azure Active Directory: rectify/correct inaccurate or incomplete personal data and erase/delete personal data/user profiles</span></span>

<span data-ttu-id="37e24-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) 是 Microsoft 的雲端式、多租用戶目錄和身分識別管理服務。</span><span class="sxs-lookup"><span data-stu-id="37e24-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) is Microsoft’s cloud-based, multi-tenant directory and identity management service.</span></span>
<span data-ttu-id="37e24-123">您可以更正、 更新或刪除客戶和員工的使用者設定檔與使用者工作資訊中包含個人資料，例如使用者名稱、 工作標題、 地址或電話號碼，您[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD)環境使用 hello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="37e24-123">You can correct, update, or delete customer and employee user profiles and user work information that contain personal data, such as a user’s name, work title, address, or phone number, in your [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) environment by using hello [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="37e24-124">您必須使用屬於 hello 目錄全域管理員帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="37e24-124">You must sign in with an account that’s a global admin for hello directory.</span></span>

#### <a name="how-do-i-correct-or-update-user-profile-and-work-information-in-azure-active-directory"></a><span data-ttu-id="37e24-125">如何在 Azure Active Directory 中更正或更新使用者設定檔和工作資訊？</span><span class="sxs-lookup"><span data-stu-id="37e24-125">How do I correct or update user profile and work information in Azure Active Directory?</span></span>

1. <span data-ttu-id="37e24-126">登入 toohello [Azure 入口網站](https://portal.azure.com)hello 目錄的全域管理員的帳戶。</span><span class="sxs-lookup"><span data-stu-id="37e24-126">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>

2. <span data-ttu-id="37e24-127">選取**更多服務**，輸入**使用者和群組**在 hello 文字方塊中，然後選取  **Enter**。</span><span class="sxs-lookup"><span data-stu-id="37e24-127">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

    ![media/image1.png](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="37e24-129">在 hello**使用者和群組**刀鋒視窗中，選取**使用者**。</span><span class="sxs-lookup"><span data-stu-id="37e24-129">On hello **Users and groups** blade, select **Users**.</span></span>

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="37e24-131">在 [hello**使用者和群組的使用者**刀鋒視窗中，從 [hello] 清單中，選取使用者，然後用 hello 選使用者的 hello] 刀鋒視窗，選取**設定檔**tooview hello 使用者設定檔資訊需要更正 toobe或更新。</span><span class="sxs-lookup"><span data-stu-id="37e24-131">On hello **Users and groups - Users** blade, select a user from hello list, and then, on hello blade for hello selected user, select **Profile** tooview hello user profile information that needs toobe corrected or updated.</span></span>

    ![media/image3.png](media/manage-personal-data-azure/image005.png)

5. <span data-ttu-id="37e24-133">修正或更新 hello 資訊，然後 hello 命令列中，選取**儲存。**</span><span class="sxs-lookup"><span data-stu-id="37e24-133">Correct or update hello information, and then, in hello command bar, select **Save.**</span></span>

6.  <span data-ttu-id="37e24-134">在 hello 選使用者的 hello 刀鋒視窗，選取 **工作資訊**tooview 使用者工作的資訊需要 toobe 修正或更新。</span><span class="sxs-lookup"><span data-stu-id="37e24-134">On hello blade for hello selected user, select **Work Info** tooview user work information that needs toobe corrected or updated.</span></span>

    ![media/image4.png](media/manage-personal-data-azure/image007.png)

7. <span data-ttu-id="37e24-136">更正或更新 hello 使用者工作的資訊，然後再，hello 命令列中，選取**儲存。**</span><span class="sxs-lookup"><span data-stu-id="37e24-136">Correct or update hello user work information, and then, in hello command bar, select **Save.**</span></span>

#### <a name="how-do-i-delete-a-user-profile-in-azure-active-directory"></a><span data-ttu-id="37e24-137">如何在 Azure Active Directory 中刪除使用者設定檔？</span><span class="sxs-lookup"><span data-stu-id="37e24-137">How do I delete a user profile in Azure Active Directory?</span></span>

1. <span data-ttu-id="37e24-138">登入 toohello [Azure 入口網站](https://portal.azure.com)hello 目錄的全域管理員的帳戶。</span><span class="sxs-lookup"><span data-stu-id="37e24-138">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>

2. <span data-ttu-id="37e24-139">選取**更多服務**，輸入**使用者和群組**在 hello 文字方塊中，然後選取  **Enter**。</span><span class="sxs-lookup"><span data-stu-id="37e24-139">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

    ![](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="37e24-140">在 hello**使用者和群組**刀鋒視窗中，選取**使用者**。</span><span class="sxs-lookup"><span data-stu-id="37e24-140">On hello **Users and groups** blade, select **Users**.</span></span>

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="37e24-142">在 hello**使用者和群組的使用者**刀鋒視窗中，選取的使用者從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="37e24-142">On hello **Users and groups - Users** blade, select a user from hello list.</span></span>

    ![media/image3.png](media/manage-personal-data-azure/image007.png)

5. <span data-ttu-id="37e24-144">在 hello 選使用者的 hello 刀鋒視窗，選取 **概觀**，然後 hello 命令列中，選取**刪除**。</span><span class="sxs-lookup"><span data-stu-id="37e24-144">On hello blade for hello selected user, select **Overview**, and then in hello command bar, select **Delete**.</span></span>

    ![](media/manage-personal-data-azure/image013.png)

### <a name="sql-database-rectifycorrect-inaccurate-or-incomplete-personal-data-erasedelete-personal-data-export-personal-data"></a><span data-ttu-id="37e24-145">SQL Database：改正/更正不正確或不完整的個人資料；清除/刪除個人資料；匯出個人資料</span><span class="sxs-lookup"><span data-stu-id="37e24-145">SQL Database: rectify/correct inaccurate or incomplete personal data; erase/delete personal data; export personal data</span></span> 

<span data-ttu-id="37e24-146">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) 是雲端資料庫，可協助開發人員建置及維護應用程式。</span><span class="sxs-lookup"><span data-stu-id="37e24-146">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) is a cloud database that helps developers build and maintain applications.</span></span>

<span data-ttu-id="37e24-147">您可以使用標準 SQL 查詢在 [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) 中更新個人資料，也可將其刪除。</span><span class="sxs-lookup"><span data-stu-id="37e24-147">Personal data can be updated in [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) using standard SQL queries, and it can also be deleted.</span></span> <span data-ttu-id="37e24-148">此外，可以從 SQL Database 使用各種不同方法，包括 hello Azure SQL Server 匯入和匯出精靈 」，並在各種不同的格式，其中包括的 BACPAC 檔案匯出個人資料。</span><span class="sxs-lookup"><span data-stu-id="37e24-148">Additionally, personal data can be exported from SQL Database using a variety of methods, including hello Azure SQL Server import and export wizard, and in a variety of formats, including a BACPAC file.</span></span>

#### <a name="how-do-i-correct-update-or-erase-personal-data-in-sql-database"></a><span data-ttu-id="37e24-149">如何更正、更新或清除 SQL Database 中的個人資料？</span><span class="sxs-lookup"><span data-stu-id="37e24-149">How do I correct, update, or erase personal data in SQL Database?</span></span>

<span data-ttu-id="37e24-150">toolearn toocorrect 或更新 SQL Database 中的個人資料如何瀏覽 hello[更新 (TRANSACT-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql)，[更新文字](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql)，[更新 with 通用資料表運算式](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql)，或[更新寫入文字](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql)文件。</span><span class="sxs-lookup"><span data-stu-id="37e24-150">toolearn how toocorrect or update personal data in SQL Database, visit hello [Update (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [Update Text](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [Update with Common Table Expression](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), or [Update Write Text](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) documentation.</span></span>

<span data-ttu-id="37e24-151">toolearn toodelete SQL Database 中的個人資料如何瀏覽 hello[刪除 (TRANSACT-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql)文件。</span><span class="sxs-lookup"><span data-stu-id="37e24-151">toolearn how toodelete personal data in SQL Database, visit hello [Delete (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) documentation.</span></span>

#### <a name="how-do-i-export-personal-data-tooa-bacpac-file-in-sql-database"></a><span data-ttu-id="37e24-152">我要如何匯出 SQL Database 中的個人資料 tooa BACPAC 檔案？</span><span class="sxs-lookup"><span data-stu-id="37e24-152">How do I export personal data tooa BACPAC file in SQL Database?</span></span>

<span data-ttu-id="37e24-153">BACPAC 檔案包含 hello SQL 資料庫資料和中繼資料，且 BACPAC 副檔名的 zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="37e24-153">A BACPAC file includes hello SQL Database data and metadata and is a zip file with a BACPAC extension.</span></span> <span data-ttu-id="37e24-154">這可以使用 hello [Azure 入口網站](https://portal.azure.com/)，hello SQLPackage 命令列公用程式、 SQL Server Management Studio (SSMS) 或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="37e24-154">This can be done using hello [Azure portal](https://portal.azure.com/), hello SQLPackage command-line utility, SQL Server Management Studio (SSMS), or PowerShell.</span></span>

<span data-ttu-id="37e24-155">toolearn 如何 tooexport 資料 tooa BACPAC 檔案，請瀏覽 hello [Azure SQL database tooa BACPAC 檔案匯出](https://docs.microsoft.com/azure/sql-database/sql-database-export)頁面，其中包括上列每個方法的詳細的指示。</span><span class="sxs-lookup"><span data-stu-id="37e24-155">toolearn how tooexport data tooa BACPAC file, visit hello [Export an Azure SQL database tooa BACPAC file](https://docs.microsoft.com/azure/sql-database/sql-database-export) page, which includes detailed instructions for each method listed above.</span></span>

<span data-ttu-id="37e24-156">如何匯出從 SQL Database 以 hello SQL Server 匯入和匯出精靈 」 的個人資料？</span><span class="sxs-lookup"><span data-stu-id="37e24-156">How do I export personal data from SQL Database with hello SQL Server Import and Export Wizard?</span></span>

<span data-ttu-id="37e24-157">此精靈可協助您將資料從來源 tooa 目的複製。</span><span class="sxs-lookup"><span data-stu-id="37e24-157">This wizard helps you copy data from a source tooa destination.</span></span> <span data-ttu-id="37e24-158">簡介 toohello 精靈 」 中，包括如何 tooget、 權限資訊，以及如何 tooget 協助 hello 工具，請瀏覽 hello[匯入和匯出資料以 hello SQL Server 匯入和匯出精靈](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard)網頁。</span><span class="sxs-lookup"><span data-stu-id="37e24-158">For an introduction toohello wizard, including how tooget it, permissions information, and how tooget help with hello tool, visit hello [Import and Export Data with hello SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) web page.</span></span>

<span data-ttu-id="37e24-159">如需 hello 精靈步驟的概觀，請瀏覽 hello [hello SQL Server 匯入和匯出精靈 」 中的步驟](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard)網頁。</span><span class="sxs-lookup"><span data-stu-id="37e24-159">For an overview of steps for hello wizard, visit hello [Steps in hello SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) web page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37e24-160">後續步驟：</span><span class="sxs-lookup"><span data-stu-id="37e24-160">Next Steps:</span></span>

[<span data-ttu-id="37e24-161">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="37e24-161">Azure SQL Database</span></span>](https://azure.microsoft.com/services/sql-database/?v=16.50) 

[<span data-ttu-id="37e24-162">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37e24-162">Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

