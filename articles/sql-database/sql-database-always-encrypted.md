---
title: "一律加密：Azure SQL Database - Windows 憑證存放區 | Microsoft Docs"
description: "本文說明如何使用 SQL Server Management Studio (SSMS) 中的 [一律加密精靈]，藉由資料庫加密來保護 SQL Database 中的機密資料。 它也會說明如何將您的加密金鑰儲存在 Windows 憑證存放區中。"
keywords: "加密資料, SQL 加密, 資料庫加密, 機密資料, 一律加密"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: ce7e052e-8bf6-4d7c-9204-4c6f4afeba4b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: sstein
ms.openlocfilehash: d1fdfc4f739e65ff532b159eefaffe1622ad0963
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-the-windows-certificate-store"></a><span data-ttu-id="a0170-105">一律加密：保護 SQL Database 中的機密資料，並將加密金鑰儲存在 Windows 憑證存放區中</span><span class="sxs-lookup"><span data-stu-id="a0170-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in the Windows certificate store</span></span>

<span data-ttu-id="a0170-106">本文說明如何使用 [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx) 中的[一律加密精靈](https://msdn.microsoft.com/library/mt459280.aspx)，藉由資料庫加密來保護 SQL Database 中的機密資料。</span><span class="sxs-lookup"><span data-stu-id="a0170-106">This article shows you how to secure sensitive data in a SQL database with database encryption by using the [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="a0170-107">它也會說明如何將您的加密金鑰儲存在 Windows 憑證存放區中。</span><span class="sxs-lookup"><span data-stu-id="a0170-107">It also shows you how to store your encryption keys in the Windows certificate store.</span></span>

<span data-ttu-id="a0170-108">「一律加密」是 Azure SQL Database 和 SQL Server 中新的資料加密技術，不論是當機密資料在伺服器上待用時、在用戶端與伺服器之間移動時，還是使用中時，都可協助保護資料，確保機密資料在資料庫系統內一律不會以純文字顯示。</span><span class="sxs-lookup"><span data-stu-id="a0170-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on the server, during movement between client and server, and while the data is in use, ensuring that sensitive data never appears as plaintext inside the database system.</span></span> <span data-ttu-id="a0170-109">加密資料之後，只有具備金鑰存取權的用戶端應用程式或應用程式伺服器才可以存取純文字資料。</span><span class="sxs-lookup"><span data-stu-id="a0170-109">After you encrypt data, only client applications or app servers that have access to the keys can access plaintext data.</span></span> <span data-ttu-id="a0170-110">如需詳細資訊，請參閱 [一律加密 (資料庫引擎)](https://msdn.microsoft.com/library/mt163865.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a0170-110">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="a0170-111">將資料庫設定為使用「一律加密」之後，您將使用 Visual Studio 以 C# 建立用戶端應用程式來使用加密資料。</span><span class="sxs-lookup"><span data-stu-id="a0170-111">After configuring the database to use Always Encrypted, you will create a client application in C# with Visual Studio to work with the encrypted data.</span></span>

<span data-ttu-id="a0170-112">請依照本文章中的步驟操作，以了解如何為 Azure SQL Database 設定「一律加密」。</span><span class="sxs-lookup"><span data-stu-id="a0170-112">Follow the steps in this article to learn how to set up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="a0170-113">在本文章中，您將學習到如何執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="a0170-113">In this article, you will learn how to perform the following tasks:</span></span>

* <span data-ttu-id="a0170-114">使用 SSMS 中的「一律加密」精靈來建立 [一律加密的金鑰](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3)。</span><span class="sxs-lookup"><span data-stu-id="a0170-114">Use the Always Encrypted wizard in SSMS to create [Always Encrypted Keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="a0170-115">建立 [資料行主要金鑰 (CMK)](https://msdn.microsoft.com/library/mt146393.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a0170-115">Create a [Column Master Key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="a0170-116">建立 [資料行加密金鑰 (CEK)](https://msdn.microsoft.com/library/mt146372.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a0170-116">Create a [Column Encryption Key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="a0170-117">建立資料庫資料表並將資料行加密。</span><span class="sxs-lookup"><span data-stu-id="a0170-117">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="a0170-118">建立可插入、選取及顯示加密資料行資料的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a0170-118">Create an application that inserts, selects, and displays data from the encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0170-119">必要條件</span><span class="sxs-lookup"><span data-stu-id="a0170-119">Prerequisites</span></span>
<span data-ttu-id="a0170-120">針對本教學課程，您將需要：</span><span class="sxs-lookup"><span data-stu-id="a0170-120">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="a0170-121">Azure 帳戶和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a0170-121">An Azure account and subscription.</span></span> <span data-ttu-id="a0170-122">如果您沒有帳戶，請註冊 [免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="a0170-122">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a0170-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 13.0.700.242 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="a0170-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="a0170-124">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) 或更新版本 (於用戶端電腦上)。</span><span class="sxs-lookup"><span data-stu-id="a0170-124">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on the client computer).</span></span>
* <span data-ttu-id="a0170-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a0170-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>

## <a name="create-a-blank-sql-database"></a><span data-ttu-id="a0170-126">建立空白 SQL Database</span><span class="sxs-lookup"><span data-stu-id="a0170-126">Create a blank SQL database</span></span>
1. <span data-ttu-id="a0170-127">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="a0170-127">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a0170-128">按一下 [新增]  >  [資料 + 儲存體]  >  [SQL Database]。</span><span class="sxs-lookup"><span data-stu-id="a0170-128">Click **New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="a0170-129">在新的或現有伺服器上建立名稱為 **Clinic** (診所) 的**空白**資料庫。</span><span class="sxs-lookup"><span data-stu-id="a0170-129">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="a0170-130">如需有關如何在 Azure 入口網站中建立資料庫的詳細指示，請參閱[您的第一個 Azure SQL Database](sql-database-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="a0170-130">For detailed instructions about creating a database in the Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![建立空白資料庫](./media/sql-database-always-encrypted/create-database.png)

<span data-ttu-id="a0170-132">在本教學課程稍後，您將會需要連接字串。</span><span class="sxs-lookup"><span data-stu-id="a0170-132">You will need the connection string later in the tutorial.</span></span> <span data-ttu-id="a0170-133">在建立資料庫之後，請移至新的 Clinic 資料庫並複製連接字串。</span><span class="sxs-lookup"><span data-stu-id="a0170-133">After the database is created, go to the new Clinic database and copy the connection string.</span></span> <span data-ttu-id="a0170-134">您可以隨時取得連接字串，但當您在 Azure 入口網站中時，很容易就可以複製它。</span><span class="sxs-lookup"><span data-stu-id="a0170-134">You can get the connection string at any time, but it's easy to copy it when you're in the Azure portal.</span></span>

1. <span data-ttu-id="a0170-135">按一下 [SQL Database]  >  [Clinic]  >  [顯示資料庫連接字串]。</span><span class="sxs-lookup"><span data-stu-id="a0170-135">Click **SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="a0170-136">複製 **ADO.NET**的連接字串。</span><span class="sxs-lookup"><span data-stu-id="a0170-136">Copy the connection string for **ADO.NET**.</span></span>
   
    ![複製連接字串](./media/sql-database-always-encrypted/connection-strings.png)

## <a name="connect-to-the-database-with-ssms"></a><span data-ttu-id="a0170-138">使用 SSMS 連接到資料庫</span><span class="sxs-lookup"><span data-stu-id="a0170-138">Connect to the database with SSMS</span></span>
<span data-ttu-id="a0170-139">開啟 SSMS 並連接到包含實務課程資料庫的伺服器。</span><span class="sxs-lookup"><span data-stu-id="a0170-139">Open SSMS and connect to the server with the Clinic database.</span></span>

1. <span data-ttu-id="a0170-140">開啟 SSMS。</span><span class="sxs-lookup"><span data-stu-id="a0170-140">Open SSMS.</span></span> <span data-ttu-id="a0170-141">(按一下 [連接]  >  [資料庫引擎] 以開啟 [連接到伺服器] 視窗 (如果此視窗未開啟))。</span><span class="sxs-lookup"><span data-stu-id="a0170-141">(Click **Connect** > **Database Engine** to open the **Connect to Server** window if it is not open).</span></span>
2. <span data-ttu-id="a0170-142">輸入您的伺服器名稱和認證。</span><span class="sxs-lookup"><span data-stu-id="a0170-142">Enter your server name and credentials.</span></span> <span data-ttu-id="a0170-143">可以在 SQL 資料庫刀鋒視窗上找到此伺服器名稱和稍早複製的連接字串。</span><span class="sxs-lookup"><span data-stu-id="a0170-143">The server name can be found on the SQL database blade and in the connection string you copied earlier.</span></span> <span data-ttu-id="a0170-144">輸入完整的伺服器名稱，包括 *database.windows.net*。</span><span class="sxs-lookup"><span data-stu-id="a0170-144">Type the complete server name including *database.windows.net*.</span></span>
   
    ![複製連接字串](./media/sql-database-always-encrypted/ssms-connect.png)

<span data-ttu-id="a0170-146">如果 [新增防火牆規則]  視窗開啟，請登入 Azure，讓 SSMS 為您建立新的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="a0170-146">If the **New Firewall Rule** window opens, sign in to Azure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="a0170-147">建立資料表</span><span class="sxs-lookup"><span data-stu-id="a0170-147">Create a table</span></span>
<span data-ttu-id="a0170-148">在本節中，您將建立資料表來保存病患的資料。</span><span class="sxs-lookup"><span data-stu-id="a0170-148">In this section, you will create a table to hold patient data.</span></span> <span data-ttu-id="a0170-149">這一開始會是一般表格 -- 您將在下一節中設定加密。</span><span class="sxs-lookup"><span data-stu-id="a0170-149">This will be a normal table initially--you will configure encryption in the next section.</span></span>

1. <span data-ttu-id="a0170-150">展開 [資料庫] 。</span><span class="sxs-lookup"><span data-stu-id="a0170-150">Expand **Databases**.</span></span>
2. <span data-ttu-id="a0170-151">在 [Clinic] 資料庫上按一下滑鼠右鍵，然後按一下 [新增查詢]。</span><span class="sxs-lookup"><span data-stu-id="a0170-151">Right-click the **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="a0170-152">將下列 Transact-SQL (T-SQL) 貼到新的查詢視窗中並「執行」  它。</span><span class="sxs-lookup"><span data-stu-id="a0170-152">Paste the following Transact-SQL (T-SQL) into the new query window and **Execute** it.</span></span>

        CREATE TABLE [dbo].[Patients](
         [PatientId] [int] IDENTITY(1,1),
         [SSN] [char](11) NOT NULL,
         [FirstName] [nvarchar](50) NULL,
         [LastName] [nvarchar](50) NULL,
         [MiddleName] [nvarchar](50) NULL,
         [StreetAddress] [nvarchar](50) NULL,
         [City] [nvarchar](50) NULL,
         [ZipCode] [char](5) NULL,
         [State] [char](2) NULL,
         [BirthDate] [date] NOT NULL
         PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] );
         GO


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="a0170-153">將資料行加密 (設定「一律加密」)</span><span class="sxs-lookup"><span data-stu-id="a0170-153">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="a0170-154">SSMS 提供一個精靈，可為您設定 CMK、CEK 及加密的資料行，來協助您輕鬆設定「一律加密」。</span><span class="sxs-lookup"><span data-stu-id="a0170-154">SSMS provides a wizard to easily configure Always Encrypted by setting up the CMK, CEK, and encrypted columns for you.</span></span>

1. <span data-ttu-id="a0170-155">展開 [資料庫]  > **空白** > ，藉由資料庫加密來保護 SQL Database 中的機密資料。</span><span class="sxs-lookup"><span data-stu-id="a0170-155">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="a0170-156">在 [Patients] 資料表上按一下滑鼠右鍵，然後選取 [加密資料行] 以開啟「一律加密精靈」：</span><span class="sxs-lookup"><span data-stu-id="a0170-156">Right-click the **Patients** table and select **Encrypt Columns** to open the Always Encrypted wizard:</span></span>
   
    ![加密資料行](./media/sql-database-always-encrypted/encrypt-columns.png)

<span data-ttu-id="a0170-158">「一律加密」精靈包含下列區段︰[資料行選取]、[主要金鑰組態] \(CMK)、[驗證] 及 [摘要]。</span><span class="sxs-lookup"><span data-stu-id="a0170-158">The Always Encrypted wizard includes the following sections: **Column Selection**, **Master Key Configuration** (CMK), **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="a0170-159">資料行選取</span><span class="sxs-lookup"><span data-stu-id="a0170-159">Column Selection</span></span>
<span data-ttu-id="a0170-160">在 [簡介] 頁面上按 [下一步]，即可開啟 [資料行選取] 頁面。</span><span class="sxs-lookup"><span data-stu-id="a0170-160">Click **Next** on the **Introduction** page to open the **Column Selection** page.</span></span> <span data-ttu-id="a0170-161">在此頁面上，您將選取要加密的資料行、 [加密類型及要使用的資料行加密金鑰 (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) 。</span><span class="sxs-lookup"><span data-stu-id="a0170-161">On this page, you will select which columns you want to encrypt, [the type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) to use.</span></span>

<span data-ttu-id="a0170-162">請加密每個病患的 **SSN** 和 **BirthDate** 資訊。</span><span class="sxs-lookup"><span data-stu-id="a0170-162">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="a0170-163">**SSN** 資料行將使用決定性加密，這可支援等式查閱、聯結及群組依據。</span><span class="sxs-lookup"><span data-stu-id="a0170-163">The **SSN** column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="a0170-164">**BirthDate** 資料行將使用不支援操作的隨機加密。</span><span class="sxs-lookup"><span data-stu-id="a0170-164">The **BirthDate** column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="a0170-165">將 **SSN** 資料行的 [加密類型] 設定為 [決定性]，並將 **BirthDate** 資料行設定為 [隨機化]。</span><span class="sxs-lookup"><span data-stu-id="a0170-165">Set the **Encryption Type** for the **SSN** column to **Deterministic** and the **BirthDate** column to **Randomized**.</span></span> <span data-ttu-id="a0170-166">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a0170-166">Click **Next**.</span></span>

![加密資料行](./media/sql-database-always-encrypted/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="a0170-168">主要金鑰組態</span><span class="sxs-lookup"><span data-stu-id="a0170-168">Master Key Configuration</span></span>
<span data-ttu-id="a0170-169">您可以在 [主要金鑰組態]  頁面設定 CMK，以及選取要用來儲存 CMK 的金鑰存放區提供者。</span><span class="sxs-lookup"><span data-stu-id="a0170-169">The **Master Key Configuration** page is where you set up your CMK and select the key store provider where the CMK will be stored.</span></span> <span data-ttu-id="a0170-170">目前，您可以將 CMK 儲存在 Windows 憑證存放區、「Azure 金鑰保存庫」或硬體安全性模組 (HSM) 中。</span><span class="sxs-lookup"><span data-stu-id="a0170-170">Currently, you can store a CMK in the Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span> <span data-ttu-id="a0170-171">本教學課程說明如何在 Windows 憑證存放區中儲存您的金鑰。</span><span class="sxs-lookup"><span data-stu-id="a0170-171">This tutorial shows how to store your keys in the Windows certificate store.</span></span>

<span data-ttu-id="a0170-172">確認已選取 [Windows 憑證存放區]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a0170-172">Verify that **Windows certificate store** is selected and click **Next**.</span></span>

![主要金鑰組態](./media/sql-database-always-encrypted/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="a0170-174">驗證</span><span class="sxs-lookup"><span data-stu-id="a0170-174">Validation</span></span>
<span data-ttu-id="a0170-175">您現在可以加密資料行，或儲存為 PowerShell 指令碼以供日後執行。</span><span class="sxs-lookup"><span data-stu-id="a0170-175">You can encrypt the columns now or save a PowerShell script to run later.</span></span> <span data-ttu-id="a0170-176">針對這個教學課程，請選取 [繼續以立即完成]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a0170-176">For this tutorial, select **Proceed to finish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="a0170-177">摘要</span><span class="sxs-lookup"><span data-stu-id="a0170-177">Summary</span></span>
<span data-ttu-id="a0170-178">確認設定全都正確，然後按一下 [完成]  以完成 [一律加密] 的設定。</span><span class="sxs-lookup"><span data-stu-id="a0170-178">Verify that the settings are all correct and click **Finish** to complete the setup for Always Encrypted.</span></span>

![摘要](./media/sql-database-always-encrypted/summary.png)

### <a name="verify-the-wizards-actions"></a><span data-ttu-id="a0170-180">確認精靈的動作</span><span class="sxs-lookup"><span data-stu-id="a0170-180">Verify the wizard's actions</span></span>
<span data-ttu-id="a0170-181">完成精靈步驟之後，您的資料庫便已完成「一律加密」設定。</span><span class="sxs-lookup"><span data-stu-id="a0170-181">After the wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="a0170-182">精靈已執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="a0170-182">The wizard performed the following actions:</span></span>

* <span data-ttu-id="a0170-183">建立 CMK。</span><span class="sxs-lookup"><span data-stu-id="a0170-183">Created a CMK.</span></span>
* <span data-ttu-id="a0170-184">建立 CEK。</span><span class="sxs-lookup"><span data-stu-id="a0170-184">Created a CEK.</span></span>
* <span data-ttu-id="a0170-185">設定選取的資料行以進行加密。</span><span class="sxs-lookup"><span data-stu-id="a0170-185">Configured the selected columns for encryption.</span></span> <span data-ttu-id="a0170-186">**Patients** 資料表目前沒有任何資料，但在所選資料行中的所有現有資料現在都已加密。</span><span class="sxs-lookup"><span data-stu-id="a0170-186">Your **Patients** table currently has no data, but any existing data in the selected columns is now encrypted.</span></span>

<span data-ttu-id="a0170-187">您可以確認 SSMS 中是否已建立金鑰，方法是移至 [Clinic]  >  [安全性]  >  [一律加密的金鑰]。</span><span class="sxs-lookup"><span data-stu-id="a0170-187">You can verify the creation of the keys in SSMS by going to **Clinic** > **Security** > **Always Encrypted Keys**.</span></span> <span data-ttu-id="a0170-188">您現在可以看到精靈為您產生的新金鑰。</span><span class="sxs-lookup"><span data-stu-id="a0170-188">You can now see the new keys that the wizard generated for you.</span></span>

## <a name="create-a-client-application-that-works-with-the-encrypted-data"></a><span data-ttu-id="a0170-189">建立搭配加密資料使用的用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="a0170-189">Create a client application that works with the encrypted data</span></span>
<span data-ttu-id="a0170-190">既然已設定好「一律加密」，您現在即可建置會在加密資料行上執行「插入」和「選取」動作的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a0170-190">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on the encrypted columns.</span></span> <span data-ttu-id="a0170-191">若要成功執行範例應用程式，您必須在您執行「一律加密」精靈的相同電腦上執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="a0170-191">To successfully run the sample application, you must run it on the same computer where you ran the Always Encrypted wizard.</span></span> <span data-ttu-id="a0170-192">若要在另一部電腦上執行該應用程式，就必須將您的「一律加密」憑證部署到執行用戶端應用程式的電腦上。</span><span class="sxs-lookup"><span data-stu-id="a0170-192">To run the application on another computer, you must deploy your Always Encrypted certificates to the computer running the client app.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="a0170-193">傳送純文字資料至具有 [一律加密] 資料行的伺服器時，您的應用程式必須使用 [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) 物件。</span><span class="sxs-lookup"><span data-stu-id="a0170-193">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data to the server with Always Encrypted columns.</span></span> <span data-ttu-id="a0170-194">在不使用 SqlParameter 物件的情況下傳遞常值會導致例外狀況。</span><span class="sxs-lookup"><span data-stu-id="a0170-194">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="a0170-195">開啟 Visual Studio，建立新的 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="a0170-195">Open Visual Studio and create a new C# console application.</span></span> <span data-ttu-id="a0170-196">請確定您的專案設定為 **.NET Framework 4.6** 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="a0170-196">Make sure your project is set to **.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="a0170-197">將專案命名為 **AlwaysEncryptedConsoleApp**，並按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="a0170-197">Name the project **AlwaysEncryptedConsoleApp** and click **OK**.</span></span>

![新的主控台應用程式](./media/sql-database-always-encrypted/console-app.png)

## <a name="modify-your-connection-string-to-enable-always-encrypted"></a><span data-ttu-id="a0170-199">修改連接字串，以啟用 [一律加密]</span><span class="sxs-lookup"><span data-stu-id="a0170-199">Modify your connection string to enable Always Encrypted</span></span>
<span data-ttu-id="a0170-200">本節說明如何在您的資料庫連接字串中啟用「一律加密」。</span><span class="sxs-lookup"><span data-stu-id="a0170-200">This section explains how to enable Always Encrypted in your database connection string.</span></span> <span data-ttu-id="a0170-201">在下一節＜一律加密範例主控台應用程式＞中，您將修改您剛剛建立的主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="a0170-201">You will modify the console app you just created in the next section, "Always Encrypted sample console application."</span></span>

<span data-ttu-id="a0170-202">若要啟用「一律加密」，您必須將 **Column Encryption Setting** 關鍵字新增到您的連接字串中，並將它設定為 **Enabled**。</span><span class="sxs-lookup"><span data-stu-id="a0170-202">To enable Always Encrypted, you need to add the **Column Encryption Setting** keyword to your connection string and set it to **Enabled**.</span></span>

<span data-ttu-id="a0170-203">您可以直接在連接字串中進行此設定，或是使用 [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx)來設定它。</span><span class="sxs-lookup"><span data-stu-id="a0170-203">You can set this directly in the connection string, or you can set it by using a [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="a0170-204">下一節中的範例應用程式會示範如何使用 **SqlConnectionStringBuilder**。</span><span class="sxs-lookup"><span data-stu-id="a0170-204">The sample application in the next section shows how to use **SqlConnectionStringBuilder**.</span></span>

> [!NOTE]
> <span data-ttu-id="a0170-205">這是 [一律加密] 特定的用戶端應用程式中唯一需要做的變更。</span><span class="sxs-lookup"><span data-stu-id="a0170-205">This is the only change required in a client application specific to Always Encrypted.</span></span> <span data-ttu-id="a0170-206">如果您有將連接字串儲存於外部 (例如儲存在組態檔中) 的現有應用程式，您或許能夠在不需變更任何程式碼的情況下啟用「一律加密」。</span><span class="sxs-lookup"><span data-stu-id="a0170-206">If you have an existing application that stores its connection string externally (that is, in a config file), you might be able to enable Always Encrypted without changing any code.</span></span>
> 
> 

### <a name="enable-always-encrypted-in-the-connection-string"></a><span data-ttu-id="a0170-207">在連接字串中啟用 [一律加密]</span><span class="sxs-lookup"><span data-stu-id="a0170-207">Enable Always Encrypted in the connection string</span></span>
<span data-ttu-id="a0170-208">在連接字串中加入下列關鍵字：</span><span class="sxs-lookup"><span data-stu-id="a0170-208">Add the following keyword to your connection string:</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-a-sqlconnectionstringbuilder"></a><span data-ttu-id="a0170-209">使用 SqlConnectionStringBuilder 啟用一律加密</span><span class="sxs-lookup"><span data-stu-id="a0170-209">Enable Always Encrypted with a SqlConnectionStringBuilder</span></span>
<span data-ttu-id="a0170-210">下列程式碼示範如何將 [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) 設定為 [Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx) 來啟用「一律加密」。</span><span class="sxs-lookup"><span data-stu-id="a0170-210">The following code shows how to enable Always Encrypted by setting the [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) to [Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="a0170-211">一律加密範例主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="a0170-211">Always Encrypted sample console application</span></span>
<span data-ttu-id="a0170-212">這個範例會示範如何：</span><span class="sxs-lookup"><span data-stu-id="a0170-212">This sample demonstrates how to:</span></span>

* <span data-ttu-id="a0170-213">修改連接字串，以啟用 [一律加密]。</span><span class="sxs-lookup"><span data-stu-id="a0170-213">Modify your connection string to enable Always Encrypted.</span></span>
* <span data-ttu-id="a0170-214">將資料插入加密資料行。</span><span class="sxs-lookup"><span data-stu-id="a0170-214">Insert data into the encrypted columns.</span></span>
* <span data-ttu-id="a0170-215">在加密資料行中篩選特定值來選取記錄。</span><span class="sxs-lookup"><span data-stu-id="a0170-215">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="a0170-216">以下列程式碼取代 **Program.cs** 的內容。</span><span class="sxs-lookup"><span data-stu-id="a0170-216">Replace the contents of **Program.cs** with the following code.</span></span> <span data-ttu-id="a0170-217">從 Azure 入口網站，針對 Main 方法上一行中的全域 connectionString 變數，使用有效的連接字串來取代其連接字串。</span><span class="sxs-lookup"><span data-stu-id="a0170-217">Replace the connection string for the global connectionString variable in the line directly above the Main method with your valid connection string from the Azure portal.</span></span> <span data-ttu-id="a0170-218">這是此程式碼唯一需要進行的變更。</span><span class="sxs-lookup"><span data-stu-id="a0170-218">This is the only change you need to make to this code.</span></span>

<span data-ttu-id="a0170-219">執行應用程式以查看「一律加密」的運作情況。</span><span class="sxs-lookup"><span data-stu-id="a0170-219">Run the app to see Always Encrypted in action.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;

    namespace AlwaysEncryptedConsoleApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from the Azure portal.
        static string connectionString = @"Replace with your connection string";

        static void Main(string[] args)
        {
            Console.WriteLine("Original connection string copied from the Azure portal:");
            Console.WriteLine(connectionString);

            // Create a SqlConnectionStringBuilder.
            SqlConnectionStringBuilder connStringBuilder =
                new SqlConnectionStringBuilder(connectionString);

            // Enable Always Encrypted for the connection.
            // This is the only change specific to Always Encrypted
            connStringBuilder.ColumnEncryptionSetting =
                SqlConnectionColumnEncryptionSetting.Enabled;

            Console.WriteLine(Environment.NewLine + "Updated connection string with Always Encrypted enabled:");
            Console.WriteLine(connStringBuilder.ConnectionString);

            // Update the connection string with a password supplied at runtime.
            Console.WriteLine(Environment.NewLine + "Enter server password:");
            connStringBuilder.Password = Console.ReadLine();


            // Assign the updated connection string to our global variable.
            connectionString = connStringBuilder.ConnectionString;


            // Delete all records to restart this demo app.
            ResetPatientsTable();

            // Add sample data to the Patients table.
            Console.Write(Environment.NewLine + "Adding sample patient data to the database...");

            InsertPatient(new Patient() {
                SSN = "999-99-0001", FirstName = "Orlando", LastName = "Gee", BirthDate = DateTime.Parse("01/04/1964") });
            InsertPatient(new Patient() {
                SSN = "999-99-0002", FirstName = "Keith", LastName = "Harris", BirthDate = DateTime.Parse("06/20/1977") });
            InsertPatient(new Patient() {
                SSN = "999-99-0003", FirstName = "Donna", LastName = "Carreras", BirthDate = DateTime.Parse("02/09/1973") });
            InsertPatient(new Patient() {
                SSN = "999-99-0004", FirstName = "Janet", LastName = "Gates", BirthDate = DateTime.Parse("08/31/1985") });
            InsertPatient(new Patient() {
                SSN = "999-99-0005", FirstName = "Lucy", LastName = "Harrington", BirthDate = DateTime.Parse("05/06/1993") });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All the records currently in the Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now let's locate records by searching the encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that the user entered 11 characters.
            // In production be sure to check all user input and use the best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 123-45-6789):");
                ssn = Console.ReadLine();
            } while (ssn.Length != 11);

            // The example allows duplicate SSN entries so we will return all records
            // that match the provided value and store the results in selectedPatients.
            Patient selectedPatient = SelectPatientBySSN(ssn);

            // Check if any records were returned and display our query results.
            if (selectedPatient != null)
            {
                Console.WriteLine("Patient found with SSN = " + ssn);
                Console.WriteLine(selectedPatient.FirstName + " " + selectedPatient.LastName + "\tSSN: "
                    + selectedPatient.SSN + "\tBirthdate: " + selectedPatient.BirthDate);
            }
            else
            {
                Console.WriteLine("No patients found with SSN = " + ssn);
            }

            Console.WriteLine("Press Enter to exit...");
            Console.ReadLine();
        }


        static int InsertPatient(Patient newPatient)
        {
            int returnValue = 0;

            string sqlCmdText = @"INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate])
         VALUES (@SSN, @FirstName, @LastName, @BirthDate);";

            SqlCommand sqlCmd = new SqlCommand(sqlCmdText);


            SqlParameter paramSSN = new SqlParameter(@"@SSN", newPatient.SSN);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            SqlParameter paramFirstName = new SqlParameter(@"@FirstName", newPatient.FirstName);
            paramFirstName.DbType = DbType.String;
            paramFirstName.Direction = ParameterDirection.Input;

            SqlParameter paramLastName = new SqlParameter(@"@LastName", newPatient.LastName);
            paramLastName.DbType = DbType.String;
            paramLastName.Direction = ParameterDirection.Input;

            SqlParameter paramBirthDate = new SqlParameter(@"@BirthDate", newPatient.BirthDate);
            paramBirthDate.SqlDbType = SqlDbType.Date;
            paramBirthDate.Direction = ParameterDirection.Input;

            sqlCmd.Parameters.Add(paramSSN);
            sqlCmd.Parameters.Add(paramFirstName);
            sqlCmd.Parameters.Add(paramLastName);
            sqlCmd.Parameters.Add(paramBirthDate);

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();
                }
                catch (Exception ex)
                {
                    returnValue = 1;
                    Console.WriteLine("The following error was encountered: ");
                    Console.WriteLine(ex.Message);
                    Console.WriteLine(Environment.NewLine + "Press Enter key to exit");
                    Console.ReadLine();
                    Environment.Exit(0);
                }
            }
            return returnValue;
        }


        static List<Patient> SelectAllPatients()
        {
            List<Patient> patients = new List<Patient>();


            SqlCommand sqlCmd = new SqlCommand(
              "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients]",
                new SqlConnection(connectionString));


            using (sqlCmd.Connection = new SqlConnection(connectionString))

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patients.Add(new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            });
                        }
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }

            return patients;
        }


        static Patient SelectPatientBySSN(string ssn)
        {
            Patient patient = new Patient();

            SqlCommand sqlCmd = new SqlCommand(
                "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN]=@SSN",
                new SqlConnection(connectionString));

            SqlParameter paramSSN = new SqlParameter(@"@SSN", ssn);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            sqlCmd.Parameters.Add(paramSSN);


            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patient = new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            };
                        }
                    }
                    else
                    {
                        patient = null;
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }
            return patient;
        }


        // This method simply deletes all records in the Patients table to reset our demo.
        static int ResetPatientsTable()
        {
            int returnValue = 0;

            SqlCommand sqlCmd = new SqlCommand("DELETE FROM Patients");
            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();

                }
                catch (Exception ex)
                {
                    returnValue = 1;
                }
            }
            return returnValue;
        }
    }

    class Patient
    {
        public string SSN { get; set; }
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public DateTime BirthDate { get; set; }
    }
    }


## <a name="verify-that-the-data-is-encrypted"></a><span data-ttu-id="a0170-220">確認資料已加密</span><span class="sxs-lookup"><span data-stu-id="a0170-220">Verify that the data is encrypted</span></span>
<span data-ttu-id="a0170-221">您可以透過使用 SSMS 來查詢 **Patients** 資料，快速檢查伺服器上的實際資料是否已加密。</span><span class="sxs-lookup"><span data-stu-id="a0170-221">You can quickly check that the actual data on the server is encrypted by querying the **Patients** data with SSMS.</span></span> <span data-ttu-id="a0170-222">(使用尚未啟用資料行加密設定的目前連線)。</span><span class="sxs-lookup"><span data-stu-id="a0170-222">(Use your current connection where the column encryption setting is not yet enabled.)</span></span>

<span data-ttu-id="a0170-223">在 Clinic 資料庫上執行下列查詢。</span><span class="sxs-lookup"><span data-stu-id="a0170-223">Run the following query on the Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="a0170-224">您可以看到加密的資料行不包含任何純文字資料。</span><span class="sxs-lookup"><span data-stu-id="a0170-224">You can see that the encrypted columns do not contain any plaintext data.</span></span>

   ![新的主控台應用程式](./media/sql-database-always-encrypted/ssms-encrypted.png)

<span data-ttu-id="a0170-226">若要使用 SSMS 來存取純文字資料，您可以將 **Column Encryption Setting=enabled** 參數新增到連線中。</span><span class="sxs-lookup"><span data-stu-id="a0170-226">To use SSMS to access the plaintext data, you can add the **Column Encryption Setting=enabled** parameter to the connection.</span></span>

1. <span data-ttu-id="a0170-227">在 SSMS 中，於 [物件總管] 中您的伺服器上按一下滑鼠右鍵，然後按一下 [中斷連線]。</span><span class="sxs-lookup"><span data-stu-id="a0170-227">In SSMS, right-click your server in **Object Explorer**, and then click **Disconnect**.</span></span>
2. <span data-ttu-id="a0170-228">按一下 [連接]  >  [資料庫引擎] 以開啟 [連接到伺服器] 視窗，然後按一下 [選項]。</span><span class="sxs-lookup"><span data-stu-id="a0170-228">Click **Connect** > **Database Engine** to open the **Connect to Server** window, and then click **Options**.</span></span>
3. <span data-ttu-id="a0170-229">按一下 [其他連接參數] 並輸入 **Column Encryption Setting=enabled**。</span><span class="sxs-lookup"><span data-stu-id="a0170-229">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![新的主控台應用程式](./media/sql-database-always-encrypted/ssms-connection-parameter.png)
4. <span data-ttu-id="a0170-231">在 **Clinic** 資料庫上執行下列查詢。</span><span class="sxs-lookup"><span data-stu-id="a0170-231">Run the following query on the **Clinic** database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="a0170-232">您現在可以在加密的資料行中看到純文字資料。</span><span class="sxs-lookup"><span data-stu-id="a0170-232">You can now see the plaintext data in the encrypted columns.</span></span>

    ![新的主控台應用程式](./media/sql-database-always-encrypted/ssms-plaintext.png)



> [!NOTE]
> <span data-ttu-id="a0170-234">如果您是從另一部電腦使用 SSMS (或任何用戶端) 進行連線，它將無法存取加密金鑰，因此將無法把資料解密。</span><span class="sxs-lookup"><span data-stu-id="a0170-234">If you connect with SSMS (or any client) from a different computer, it will not have access to the encryption keys and will not be able to decrypt the data.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a0170-235">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a0170-235">Next steps</span></span>
<span data-ttu-id="a0170-236">建立使用「一律加密」的資料庫之後，您可以執行下列操作：</span><span class="sxs-lookup"><span data-stu-id="a0170-236">After you create a database that uses Always Encrypted, you may want to do the following:</span></span>

* <span data-ttu-id="a0170-237">從不同的電腦執行此範例。</span><span class="sxs-lookup"><span data-stu-id="a0170-237">Run this sample from a different computer.</span></span> <span data-ttu-id="a0170-238">它將無法存取加密金鑰，因此將無法存取純文字資料，也無法成功執行。</span><span class="sxs-lookup"><span data-stu-id="a0170-238">It won't have access to the encryption keys, so it will not have access to the plaintext data and will not run successfully.</span></span>
* <span data-ttu-id="a0170-239">[輪替和清除金鑰](https://msdn.microsoft.com/library/mt607048.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a0170-239">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="a0170-240">[移轉已經透過一律加密來加密的資料](https://msdn.microsoft.com/library/mt621539.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a0170-240">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>
* <span data-ttu-id="a0170-241">[將一律加密的憑證部署到其他用戶端電腦](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (請參閱＜讓憑證可供應用程式和使用者使用＞一節)。</span><span class="sxs-lookup"><span data-stu-id="a0170-241">[Deploy Always Encrypted certificates to other client machines](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (see the "Making Certificates Available to Applications and Users" section).</span></span>

## <a name="related-information"></a><span data-ttu-id="a0170-242">相關資訊</span><span class="sxs-lookup"><span data-stu-id="a0170-242">Related information</span></span>
* [<span data-ttu-id="a0170-243">一律加密 (用戶端開發)</span><span class="sxs-lookup"><span data-stu-id="a0170-243">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="a0170-244">透明資料加密</span><span class="sxs-lookup"><span data-stu-id="a0170-244">Transparent Data Encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="a0170-245">SQL Server 加密</span><span class="sxs-lookup"><span data-stu-id="a0170-245">SQL Server Encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="a0170-246">Always Encrypted Wizard (一律加密精靈)</span><span class="sxs-lookup"><span data-stu-id="a0170-246">Always Encrypted Wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="a0170-247">Always Encrypted Blog (一律加密部落格)</span><span class="sxs-lookup"><span data-stu-id="a0170-247">Always Encrypted Blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

