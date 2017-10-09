---
title: "永遠加密：SQL Database - Azure Key Vault | Microsoft Docs"
description: "本文章將示範如何 toosecure 資料加密使用的 SQL 資料庫中的敏感性資料 hello 永遠加密精靈 在 SQL Server Management Studio。 它也包含指示，教您如何 toostore Azure 金鑰保存庫中的每個加密金鑰。"
keywords: "資料加密, 加密金鑰, 雲端加密"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: 6ca16644-5969-497b-a413-d28c3b835c9b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: sstein
ms.openlocfilehash: 8226bfef584e979643f5bb0747d4df16569f8204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-azure-key-vault"></a><span data-ttu-id="847a5-105">一律加密：保護 SQL Database 中的機密資料，並將加密金鑰儲存在「Azure 金鑰保存庫」中</span><span class="sxs-lookup"><span data-stu-id="847a5-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in Azure Key Vault</span></span>

<span data-ttu-id="847a5-106">本文將告訴您如何 toosecure 敏感性資料，在 SQL 資料庫與資料加密使用 hello[永遠加密精靈](https://msdn.microsoft.com/library/mt459280.aspx)中[SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx)。</span><span class="sxs-lookup"><span data-stu-id="847a5-106">This article shows you how toosecure sensitive data in a SQL database with data encryption using hello [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="847a5-107">它也包含指示，教您如何 toostore Azure 金鑰保存庫中的每個加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="847a5-107">It also includes instructions that will show you how toostore each encryption key in Azure Key Vault.</span></span>

<span data-ttu-id="847a5-108">永遠加密已在 Azure SQL Database 的新資料加密技術，可幫助的 SQL Server 進行用戶端與伺服器之間，以及使用 hello 資料時移動時保護靜止 hello 伺服器上的機密資料。</span><span class="sxs-lookup"><span data-stu-id="847a5-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on hello server, during movement between client and server, and while hello data is in use.</span></span> <span data-ttu-id="847a5-109">一律加密可確保敏感性資料，永遠不會顯示為 hello 資料庫系統內的純文字。</span><span class="sxs-lookup"><span data-stu-id="847a5-109">Always Encrypted ensures that sensitive data never appears as plaintext inside hello database system.</span></span> <span data-ttu-id="847a5-110">設定資料加密之後，只有用戶端應用程式或具有存取 toohello 金鑰的應用程式伺服器可以存取純文字資料。</span><span class="sxs-lookup"><span data-stu-id="847a5-110">After you configure data encryption, only client applications or app servers that have access toohello keys can access plaintext data.</span></span> <span data-ttu-id="847a5-111">如需詳細資訊，請參閱 [一律加密 (資料庫引擎)](https://msdn.microsoft.com/library/mt163865.aspx)。</span><span class="sxs-lookup"><span data-stu-id="847a5-111">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="847a5-112">設定永遠加密的 hello 資料庫 toouse 之後，您將建立用戶端應用程式中使用 C# 和 Visual Studio toowork hello 加密資料。</span><span class="sxs-lookup"><span data-stu-id="847a5-112">After you configure hello database toouse Always Encrypted, you will create a client application in C# with Visual Studio toowork with hello encrypted data.</span></span>

<span data-ttu-id="847a5-113">請遵循本文章中的 hello 步驟，並了解如何為 Azure SQL database 的 tooset 設定永遠加密。</span><span class="sxs-lookup"><span data-stu-id="847a5-113">Follow hello steps in this article and learn how tooset up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="847a5-114">在本文中，您將學習影響 tooperform hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="847a5-114">In this article you will learn how tooperform hello following tasks:</span></span>

* <span data-ttu-id="847a5-115">使用 SSMS toocreate 的 hello 永遠加密精靈[永遠加密金鑰](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3)。</span><span class="sxs-lookup"><span data-stu-id="847a5-115">Use hello Always Encrypted wizard in SSMS toocreate [Always Encrypted keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="847a5-116">建立 [資料行主要金鑰 (CMK)](https://msdn.microsoft.com/library/mt146393.aspx)。</span><span class="sxs-lookup"><span data-stu-id="847a5-116">Create a [column master key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="847a5-117">建立 [資料行加密金鑰 (CEK)](https://msdn.microsoft.com/library/mt146372.aspx)。</span><span class="sxs-lookup"><span data-stu-id="847a5-117">Create a [column encryption key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="847a5-118">建立資料庫資料表並將資料行加密。</span><span class="sxs-lookup"><span data-stu-id="847a5-118">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="847a5-119">建立的應用程式，將插入、 選取，並顯示 hello 加密資料行的資料。</span><span class="sxs-lookup"><span data-stu-id="847a5-119">Create an application that inserts, selects, and displays data from hello encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="847a5-120">必要條件</span><span class="sxs-lookup"><span data-stu-id="847a5-120">Prerequisites</span></span>
<span data-ttu-id="847a5-121">針對本教學課程，您將需要：</span><span class="sxs-lookup"><span data-stu-id="847a5-121">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="847a5-122">Azure 帳戶和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="847a5-122">An Azure account and subscription.</span></span> <span data-ttu-id="847a5-123">如果您沒有帳戶，請註冊 [免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="847a5-123">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="847a5-124">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 13.0.700.242 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="847a5-124">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="847a5-125">[.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx)或更新版本 （在 hello 用戶端電腦）。</span><span class="sxs-lookup"><span data-stu-id="847a5-125">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on hello client computer).</span></span>
* <span data-ttu-id="847a5-126">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)。</span><span class="sxs-lookup"><span data-stu-id="847a5-126">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>
* <span data-ttu-id="847a5-127">[Azure PowerShell](/powershell/azure/overview) 1.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="847a5-127">[Azure PowerShell](/powershell/azure/overview), version  1.0 or later.</span></span> <span data-ttu-id="847a5-128">型別**(Get-module azure ListAvailable)。版本**toosee 執行的 PowerShell 版本。</span><span class="sxs-lookup"><span data-stu-id="847a5-128">Type **(Get-Module azure -ListAvailable).Version** toosee what version of PowerShell you are running.</span></span>

## <a name="enable-your-client-application-tooaccess-hello-sql-database-service"></a><span data-ttu-id="847a5-129">啟用用戶端應用程式 tooaccess hello SQL Database 服務</span><span class="sxs-lookup"><span data-stu-id="847a5-129">Enable your client application tooaccess hello SQL Database service</span></span>
<span data-ttu-id="847a5-130">您必須啟用用戶端應用程式 tooaccess hello SQL Database 服務藉由設定 hello 必要的驗證和取得 hello *ClientId*和*密碼*，您將需要 tooauthenticate下列程式碼的 hello 中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="847a5-130">You must enable your client application tooaccess hello SQL Database service by setting up hello required authentication and acquiring hello *ClientId* and *Secret* that you will need tooauthenticate your application in hello following code.</span></span>

1. <span data-ttu-id="847a5-131">開啟 hello [Azure 傳統入口網站](http://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="847a5-131">Open hello [Azure classic portal](http://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="847a5-132">選取**Active Directory** ，按一下 應用程式將使用的 hello Active Directory 執行個體。</span><span class="sxs-lookup"><span data-stu-id="847a5-132">Select **Active Directory** and click hello Active Directory instance that your application will use.</span></span>
3. <span data-ttu-id="847a5-133">按一下 應用程式，然後按一下新增。</span><span class="sxs-lookup"><span data-stu-id="847a5-133">Click **Applications**, and then click **ADD**.</span></span>
4. <span data-ttu-id="847a5-134">輸入您的應用程式的名稱 (例如： *myClientApp*)，請選取**WEB 應用程式**，然後按一下 hello 箭號 toocontinue。</span><span class="sxs-lookup"><span data-stu-id="847a5-134">Type a name for your application (for example: *myClientApp*), select **WEB APPLICATION**, and click hello arrow toocontinue.</span></span>
5. <span data-ttu-id="847a5-135">Hello**登入 URL**和**應用程式識別碼 URI**您可以輸入有效的 URL (例如， *http://myClientApp*)，並繼續。</span><span class="sxs-lookup"><span data-stu-id="847a5-135">For hello **SIGN-ON URL** and **APP ID URI** you can type a valid URL (for example, *http://myClientApp*) and continue.</span></span>
6. <span data-ttu-id="847a5-136">按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="847a5-136">Click **CONFIGURE**.</span></span>
7. <span data-ttu-id="847a5-137">複製您的 [用戶端識別碼] 。</span><span class="sxs-lookup"><span data-stu-id="847a5-137">Copy your **CLIENT ID**.</span></span> <span data-ttu-id="847a5-138">(您之後在程式碼中將需要此值)。</span><span class="sxs-lookup"><span data-stu-id="847a5-138">(You will need this value in your code later.)</span></span>
8. <span data-ttu-id="847a5-139">在 hello**金鑰**區段中，選取**1 年**從 hello**選取持續時間**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="847a5-139">In hello **keys** section, select **1 year** from hello  **Select duration** drop-down list.</span></span> <span data-ttu-id="847a5-140">（您將可以複製 hello 金鑰之後，您將儲存在步驟 13）。</span><span class="sxs-lookup"><span data-stu-id="847a5-140">(You will copy hello key after you save in step 13.)</span></span>
9. <span data-ttu-id="847a5-141">向下捲動並按一下 [新增應用程式] 。</span><span class="sxs-lookup"><span data-stu-id="847a5-141">Scroll down and click **Add application**.</span></span>
10. <span data-ttu-id="847a5-142">保留**顯示**設定得**Microsoft 應用程式**選取**Microsoft Azure 服務管理 API**。</span><span class="sxs-lookup"><span data-stu-id="847a5-142">Leave **SHOW** set too**Microsoft Apps** and select **Microsoft Azure Service Management API**.</span></span> <span data-ttu-id="847a5-143">按一下 hello 核取記號 toocontinue。</span><span class="sxs-lookup"><span data-stu-id="847a5-143">Click hello checkmark toocontinue.</span></span>
11. <span data-ttu-id="847a5-144">選取**存取 Azure 服務管理...**從 hello**委派的權限**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="847a5-144">Select **Access Azure Service Management...** from hello **Delegated Permissions** drop-down list.</span></span>
12. <span data-ttu-id="847a5-145">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="847a5-145">Click **SAVE**.</span></span>
13. <span data-ttu-id="847a5-146">儲存完成的 hello 之後, 將 hello 索引鍵值複製 hello**金鑰**> 一節。</span><span class="sxs-lookup"><span data-stu-id="847a5-146">After hello save finishes, copy hello key value in hello **keys** section.</span></span> <span data-ttu-id="847a5-147">(您之後在程式碼中將需要此值)。</span><span class="sxs-lookup"><span data-stu-id="847a5-147">(You will need this value in your code later.)</span></span>

## <a name="create-a-key-vault-toostore-your-keys"></a><span data-ttu-id="847a5-148">您的金鑰建立金鑰保存庫 toostore</span><span class="sxs-lookup"><span data-stu-id="847a5-148">Create a key vault toostore your keys</span></span>
<span data-ttu-id="847a5-149">現在已設定您的用戶端應用程式，並可讓用戶端識別碼，它是時間 toocreate 金鑰保存庫，並設定其存取原則，讓您和您的應用程式可以存取保存庫 hello 機密資料 （hello 永遠加密金鑰）。</span><span class="sxs-lookup"><span data-stu-id="847a5-149">Now that your client app is configured and you have your client ID, it's time toocreate a key vault and configure its access policy so you and your application can access hello vault's secrets (hello Always Encrypted keys).</span></span> <span data-ttu-id="847a5-150">hello*建立*，*取得*，*清單*，*登*，*確認*， *wrapKey*，和*unwrapKey*不需要建立新的資料行主要金鑰和設定加密與 SQL Server Management Studio 的權限。</span><span class="sxs-lookup"><span data-stu-id="847a5-150">hello *create*, *get*, *list*, *sign*, *verify*, *wrapKey*, and *unwrapKey* permissions are required for creating a new column master key and for setting up encryption with SQL Server Management Studio.</span></span>

<span data-ttu-id="847a5-151">您可以執行下列指令碼的 hello，快速建立金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="847a5-151">You can quickly create a key vault by running hello following script.</span></span> <span data-ttu-id="847a5-152">如需這些 Cmdlet 的詳細說明，以及有關建立及設定金鑰保存庫的詳細資訊，請參閱[開始使用 Azure 金鑰保存庫](../key-vault/key-vault-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="847a5-152">For a detailed explanation of these cmdlets and more information about creating and configuring a key vault, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>

    $subscriptionName = '<your Azure subscription name>'
    $userPrincipalName = '<username@domain.com>'
    $clientId = '<client ID that you copied in step 7 above>'
    $resourceGroupName = '<resource group name>'
    $location = '<datacenter location>'
    $vaultName = 'AeKeyVault'


    Login-AzureRmAccount
    $subscriptionId = (Get-AzureRmSubscription -SubscriptionName $subscriptionName).Id
    Set-AzureRmContext -SubscriptionId $subscriptionId

    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    New-AzureRmKeyVault -VaultName $vaultName -ResourceGroupName $resourceGroupName -Location $location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $resourceGroupName -PermissionsToKeys create,get,wrapKey,unwrapKey,sign,verify,list -UserPrincipalName $userPrincipalName
    Set-AzureRmKeyVaultAccessPolicy  -VaultName $vaultName  -ResourceGroupName $resourceGroupName -ServicePrincipalName $clientId -PermissionsToKeys get,wrapKey,unwrapKey,sign,verify,list




## <a name="create-a-blank-sql-database"></a><span data-ttu-id="847a5-153">建立空白 SQL Database</span><span class="sxs-lookup"><span data-stu-id="847a5-153">Create a blank SQL database</span></span>
1. <span data-ttu-id="847a5-154">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="847a5-154">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="847a5-155">跳過**新增** > **資料 + 儲存體** > **SQL Database**。</span><span class="sxs-lookup"><span data-stu-id="847a5-155">Go too**New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="847a5-156">在新的或現有伺服器上建立名稱為 **Clinic** (診所) 的**空白**資料庫。</span><span class="sxs-lookup"><span data-stu-id="847a5-156">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="847a5-157">如需有關如何 toocreate 資料庫在 hello Azure 入口網站，請參閱詳細指示[第一個 Azure SQL database](sql-database-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="847a5-157">For detailed directions about how toocreate a database in hello Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![建立空白資料庫](./media/sql-database-always-encrypted-azure-key-vault/create-database.png)

<span data-ttu-id="847a5-159">連接字串將會需要 hello 稍後 hello 教學課程中，因此建立 hello 資料庫之後，請瀏覽 toohello 新實習課程資料庫和複本 hello 的連接字串。</span><span class="sxs-lookup"><span data-stu-id="847a5-159">You will need hello connection string later in hello tutorial, so after you create hello database, browse toohello new  Clinic database and copy hello connection string.</span></span> <span data-ttu-id="847a5-160">您可以在任何時間，取得 hello 連接字串，但它是簡單 toocopy hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="847a5-160">You can get hello connection string at any time, but it's easy toocopy it in hello Azure portal.</span></span>

1. <span data-ttu-id="847a5-161">跳過**SQL 資料庫** > **診所** > **顯示資料庫的連接字串**。</span><span class="sxs-lookup"><span data-stu-id="847a5-161">Go too**SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="847a5-162">複製連接字串 hello **ADO.NET**。</span><span class="sxs-lookup"><span data-stu-id="847a5-162">Copy hello connection string for **ADO.NET**.</span></span>
   
    ![複製 hello 連接字串](./media/sql-database-always-encrypted-azure-key-vault/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a><span data-ttu-id="847a5-164">使用 SSMS 連接 toohello 資料庫</span><span class="sxs-lookup"><span data-stu-id="847a5-164">Connect toohello database with SSMS</span></span>
<span data-ttu-id="847a5-165">開啟 SSMS 並連接 toohello 伺服器與 hello 診所資料庫。</span><span class="sxs-lookup"><span data-stu-id="847a5-165">Open SSMS and connect toohello server with hello Clinic database.</span></span>

1. <span data-ttu-id="847a5-166">開啟 SSMS。</span><span class="sxs-lookup"><span data-stu-id="847a5-166">Open SSMS.</span></span> <span data-ttu-id="847a5-167">(跳過**連接** > **Database Engine** tooopen hello**連接 tooServer**如果它未開啟的視窗。)</span><span class="sxs-lookup"><span data-stu-id="847a5-167">(Go too**Connect** > **Database Engine** tooopen hello **Connect tooServer** window if it isn't open.)</span></span>
2. <span data-ttu-id="847a5-168">輸入您的伺服器名稱和認證。</span><span class="sxs-lookup"><span data-stu-id="847a5-168">Enter your server name and credentials.</span></span> <span data-ttu-id="847a5-169">hello SQL 資料庫刀鋒視窗上可以找到 hello 伺服器名稱和 hello 連接字串中您之前複製。</span><span class="sxs-lookup"><span data-stu-id="847a5-169">hello server name can be found on hello SQL database blade and in hello connection string you copied earlier.</span></span> <span data-ttu-id="847a5-170">型別 hello 完整的伺服器名稱，包括*.database.windows.net*。</span><span class="sxs-lookup"><span data-stu-id="847a5-170">Type hello complete server name, including *database.windows.net*.</span></span>
   
    ![複製 hello 連接字串](./media/sql-database-always-encrypted-azure-key-vault/ssms-connect.png)

<span data-ttu-id="847a5-172">如果 hello**新防火牆規則**視窗隨即開啟，登入 tooAzure 並讓 SSMS 為您建立新的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="847a5-172">If hello **New Firewall Rule** window opens, sign in tooAzure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="847a5-173">建立資料表</span><span class="sxs-lookup"><span data-stu-id="847a5-173">Create a table</span></span>
<span data-ttu-id="847a5-174">在本節中，您將建立資料表 toohold 病患資料。</span><span class="sxs-lookup"><span data-stu-id="847a5-174">In this section, you will create a table toohold patient data.</span></span> <span data-ttu-id="847a5-175">它不是一開始加密-您將設定加密 hello 下一節。</span><span class="sxs-lookup"><span data-stu-id="847a5-175">It's not initially encrypted--you will configure encryption in hello next section.</span></span>

1. <span data-ttu-id="847a5-176">展開 [資料庫] 。</span><span class="sxs-lookup"><span data-stu-id="847a5-176">Expand **Databases**.</span></span>
2. <span data-ttu-id="847a5-177">以滑鼠右鍵按一下 hello**診所**資料庫中，按一下 **新查詢**。</span><span class="sxs-lookup"><span data-stu-id="847a5-177">Right-click hello **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="847a5-178">貼上下列 TRANSACT-SQL (T-SQL) 至新增查詢視窗 hello 的 hello 和**Execute**它。</span><span class="sxs-lookup"><span data-stu-id="847a5-178">Paste hello following Transact-SQL (T-SQL) into hello new query window and **Execute** it.</span></span>

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


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="847a5-179">將資料行加密 (設定「一律加密」)</span><span class="sxs-lookup"><span data-stu-id="847a5-179">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="847a5-180">SSMS 提供可協助您輕鬆地設定 hello 資料行主要金鑰、 資料行加密金鑰，加密的資料行的和您所設定 永遠加密的精靈。</span><span class="sxs-lookup"><span data-stu-id="847a5-180">SSMS provides a wizard that helps you easily configure Always Encrypted by setting up hello column master key, column encryption key, and encrypted columns for you.</span></span>

1. <span data-ttu-id="847a5-181">展開 [資料庫]  > **空白** > ，藉由資料庫加密來保護 SQL Database 中的機密資料。</span><span class="sxs-lookup"><span data-stu-id="847a5-181">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="847a5-182">以滑鼠右鍵按一下 hello**病患**資料表，然後選取**加密資料行**tooopen hello 永遠加密精靈：</span><span class="sxs-lookup"><span data-stu-id="847a5-182">Right-click hello **Patients** table and select **Encrypt Columns** tooopen hello Always Encrypted wizard:</span></span>
   
    ![加密資料行](./media/sql-database-always-encrypted-azure-key-vault/encrypt-columns.png)

<span data-ttu-id="847a5-184">hello 永遠加密精靈包含下列各節的 hello:**資料行選取**，**主要金鑰設定**，**驗證**，和**摘要**.</span><span class="sxs-lookup"><span data-stu-id="847a5-184">hello Always Encrypted wizard includes hello following sections: **Column Selection**, **Master Key Configuration**, **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="847a5-185">資料行選取</span><span class="sxs-lookup"><span data-stu-id="847a5-185">Column Selection</span></span>
<span data-ttu-id="847a5-186">按一下**下一步**上 hello**簡介**頁面 tooopen hello**資料行選取**頁面。</span><span class="sxs-lookup"><span data-stu-id="847a5-186">Click **Next** on hello **Introduction** page tooopen hello **Column Selection** page.</span></span> <span data-ttu-id="847a5-187">這個頁面上，您將選取的資料行要 tooencrypt， [hello 類型的加密，以及哪些資料行加密金鑰 (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse。</span><span class="sxs-lookup"><span data-stu-id="847a5-187">On this page, you will select which columns you want tooencrypt, [hello type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span></span>

<span data-ttu-id="847a5-188">請加密每個病患的 **SSN** 和 **BirthDate** 資訊。</span><span class="sxs-lookup"><span data-stu-id="847a5-188">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="847a5-189">hello SSN 資料行都將使用決定性加密，它支援等號比較查閱、 聯結和分組方式。</span><span class="sxs-lookup"><span data-stu-id="847a5-189">hello SSN column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="847a5-190">hello BirthDate 資料行，將使用隨機化的加密，不支援作業。</span><span class="sxs-lookup"><span data-stu-id="847a5-190">hello BirthDate column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="847a5-191">設定 hello**加密類型**hello SSN 資料行太**決定性**太 hello BirthDate 資料行和**隨機化**。</span><span class="sxs-lookup"><span data-stu-id="847a5-191">Set hello **Encryption Type** for hello SSN column too**Deterministic** and hello BirthDate column too**Randomized**.</span></span> <span data-ttu-id="847a5-192">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="847a5-192">Click **Next**.</span></span>

![加密資料行](./media/sql-database-always-encrypted-azure-key-vault/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="847a5-194">主要金鑰組態</span><span class="sxs-lookup"><span data-stu-id="847a5-194">Master Key Configuration</span></span>
<span data-ttu-id="847a5-195">hello**主要金鑰設定**頁面是設定您的 CMK 和選取 hello 金鑰存放區提供者 hello CMK 的儲存位置。</span><span class="sxs-lookup"><span data-stu-id="847a5-195">hello **Master Key Configuration** page is where you set up your CMK and select hello key store provider where hello CMK will be stored.</span></span> <span data-ttu-id="847a5-196">目前，您可以在 hello Windows 憑證存放區、 Azure 金鑰保存庫或硬體安全性模組 (HSM) 中儲存 CMK。</span><span class="sxs-lookup"><span data-stu-id="847a5-196">Currently, you can store a CMK in hello Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span>

<span data-ttu-id="847a5-197">本教學課程示範如何 toostore 您在 Azure 金鑰保存庫中的金鑰。</span><span class="sxs-lookup"><span data-stu-id="847a5-197">This tutorial shows how toostore your keys in Azure Key Vault.</span></span>

1. <span data-ttu-id="847a5-198">選取 [Azure 金鑰保存庫] 。</span><span class="sxs-lookup"><span data-stu-id="847a5-198">Select **Azure Key Vault**.</span></span>
2. <span data-ttu-id="847a5-199">從 hello 下拉式清單中選取 hello 所需的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="847a5-199">Select hello desired key vault from hello drop-down list.</span></span>
3. <span data-ttu-id="847a5-200">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="847a5-200">Click **Next**.</span></span>

![主要金鑰組態](./media/sql-database-always-encrypted-azure-key-vault/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="847a5-202">驗證</span><span class="sxs-lookup"><span data-stu-id="847a5-202">Validation</span></span>
<span data-ttu-id="847a5-203">您可以現在加密 hello 資料行，或稍後儲存 PowerShell 指令碼 toorun。</span><span class="sxs-lookup"><span data-stu-id="847a5-203">You can encrypt hello columns now or save a PowerShell script toorun later.</span></span> <span data-ttu-id="847a5-204">此教學課程中，選取**現在繼續 toofinish**按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="847a5-204">For this tutorial, select **Proceed toofinish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="847a5-205">摘要</span><span class="sxs-lookup"><span data-stu-id="847a5-205">Summary</span></span>
<span data-ttu-id="847a5-206">請確認 hello 設定都正確，然後按一下**完成**toocomplete hello 安裝程式的一律加密。</span><span class="sxs-lookup"><span data-stu-id="847a5-206">Verify that hello settings are all correct and click **Finish** toocomplete hello setup for Always Encrypted.</span></span>

![摘要](./media/sql-database-always-encrypted-azure-key-vault/summary.png)

### <a name="verify-hello-wizards-actions"></a><span data-ttu-id="847a5-208">確認 hello 精靈的動作</span><span class="sxs-lookup"><span data-stu-id="847a5-208">Verify hello wizard's actions</span></span>
<span data-ttu-id="847a5-209">Hello 精靈完成後，您的資料庫設定永遠加密。</span><span class="sxs-lookup"><span data-stu-id="847a5-209">After hello wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="847a5-210">hello 精靈執行 hello 下列動作：</span><span class="sxs-lookup"><span data-stu-id="847a5-210">hello wizard performed hello following actions:</span></span>

* <span data-ttu-id="847a5-211">建立資料行主要金鑰 (CMK) 並將它儲存在「Azure 金鑰保存庫」中。</span><span class="sxs-lookup"><span data-stu-id="847a5-211">Created a column master key and stored it in Azure Key Vault.</span></span>
* <span data-ttu-id="847a5-212">建立資料行加密金鑰 (CMK) 並將它儲存在「Azure 金鑰保存庫」中。</span><span class="sxs-lookup"><span data-stu-id="847a5-212">Created a column encryption key and stored it in Azure Key Vault.</span></span>
* <span data-ttu-id="847a5-213">設定的 hello 選取加密的資料行。</span><span class="sxs-lookup"><span data-stu-id="847a5-213">Configured hello selected columns for encryption.</span></span> <span data-ttu-id="847a5-214">hello 病患資料表目前有任何資料，但 hello 選取資料行中的任何現有資料已加密。</span><span class="sxs-lookup"><span data-stu-id="847a5-214">hello Patients table currently has no data, but any existing data in hello selected columns is now encrypted.</span></span>

<span data-ttu-id="847a5-215">您可以確認 hello 建立 hello 索引鍵，在 SSMS 中，展開**診所** > **安全性** > **永遠加密金鑰**。</span><span class="sxs-lookup"><span data-stu-id="847a5-215">You can verify hello creation of hello keys in SSMS by expanding **Clinic** > **Security** > **Always Encrypted Keys**.</span></span>

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a><span data-ttu-id="847a5-216">建立搭配 hello 加密資料的用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="847a5-216">Create a client application that works with hello encrypted data</span></span>
<span data-ttu-id="847a5-217">現在，永遠加密已設定，您可以建立執行的應用程式*插入*和*選取*hello 上加密的資料行。</span><span class="sxs-lookup"><span data-stu-id="847a5-217">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on hello encrypted columns.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="847a5-218">您的應用程式必須使用[SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx)物件時傳遞純文字資料 toohello server 使用永遠加密資料行。</span><span class="sxs-lookup"><span data-stu-id="847a5-218">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data toohello server with Always Encrypted columns.</span></span> <span data-ttu-id="847a5-219">在不使用 SqlParameter 物件的情況下傳遞常值會導致例外狀況。</span><span class="sxs-lookup"><span data-stu-id="847a5-219">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="847a5-220">開啟 Visual Studio 並建立新的 C# **主控台應用程式**(Visual Studio 2015 和更早版本) 或**主控台應用程式 (.NET Framework)** (Visual Studio 2017 和更新版本)。</span><span class="sxs-lookup"><span data-stu-id="847a5-220">Open Visual Studio and create a new C# **Console Application** (Visual Studio 2015 and earlier) or **Console App (.NET Framework)** (Visual Studio 2017 and later).</span></span> <span data-ttu-id="847a5-221">請確定您的專案已設定太**.NET Framework 4.6**或更新版本。</span><span class="sxs-lookup"><span data-stu-id="847a5-221">Make sure your project is set too**.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="847a5-222">名稱 hello 專案**AlwaysEncryptedConsoleAKVApp**按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="847a5-222">Name hello project **AlwaysEncryptedConsoleAKVApp** and click **OK**.</span></span>
3. <span data-ttu-id="847a5-223">安裝下列 NuGet 套件移過 hello**工具** > **NuGet 套件管理員** > **Package Manager Console**。</span><span class="sxs-lookup"><span data-stu-id="847a5-223">Install hello following NuGet packages by going too**Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="847a5-224">Hello Package Manager Console 中，執行下列兩行程式碼。</span><span class="sxs-lookup"><span data-stu-id="847a5-224">Run these two lines of code in hello Package Manager Console.</span></span>

    Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory



## <a name="modify-your-connection-string-tooenable-always-encrypted"></a><span data-ttu-id="847a5-225">修改您的連接字串 tooenable 永遠加密</span><span class="sxs-lookup"><span data-stu-id="847a5-225">Modify your connection string tooenable Always Encrypted</span></span>
<span data-ttu-id="847a5-226">本章節將說明如何在資料庫連接字串中的 tooenable 永遠加密。</span><span class="sxs-lookup"><span data-stu-id="847a5-226">This section  explains how tooenable Always Encrypted in your database connection string.</span></span>

<span data-ttu-id="847a5-227">tooenable 永遠加密，您需要 tooadd hello **Column Encryption Setting**關鍵字 tooyour 連接字串，並將它設定太**啟用**。</span><span class="sxs-lookup"><span data-stu-id="847a5-227">tooenable Always Encrypted, you need tooadd hello **Column Encryption Setting** keyword tooyour connection string and set it too**Enabled**.</span></span>

<span data-ttu-id="847a5-228">您可以直接在 hello 連接字串設定，或您可以使用來設定[SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx)。</span><span class="sxs-lookup"><span data-stu-id="847a5-228">You can set this directly in hello connection string, or you can set it by using [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="847a5-229">hello hello 範例應用程式下一節顯示如何 toouse **SqlConnectionStringBuilder**。</span><span class="sxs-lookup"><span data-stu-id="847a5-229">hello sample application in hello next section shows how toouse **SqlConnectionStringBuilder**.</span></span>

### <a name="enable-always-encrypted-in-hello-connection-string"></a><span data-ttu-id="847a5-230">Hello 連接字串中啟用 永遠加密</span><span class="sxs-lookup"><span data-stu-id="847a5-230">Enable Always Encrypted in hello connection string</span></span>
<span data-ttu-id="847a5-231">新增下列關鍵字 tooyour 連接字串 hello。</span><span class="sxs-lookup"><span data-stu-id="847a5-231">Add hello following keyword tooyour connection string.</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-sqlconnectionstringbuilder"></a><span data-ttu-id="847a5-232">使用 SqlConnectionStringBuilder 來啟用一律加密</span><span class="sxs-lookup"><span data-stu-id="847a5-232">Enable Always Encrypted with SqlConnectionStringBuilder</span></span>
<span data-ttu-id="847a5-233">hello 下列程式碼會示範如何藉由設定永遠加密的 tooenable [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx)太[啟用](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx)。</span><span class="sxs-lookup"><span data-stu-id="847a5-233">hello following code shows how tooenable Always Encrypted by setting [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) too[Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;

## <a name="register-hello-azure-key-vault-provider"></a><span data-ttu-id="847a5-234">註冊 hello Azure 金鑰保存庫提供者</span><span class="sxs-lookup"><span data-stu-id="847a5-234">Register hello Azure Key Vault provider</span></span>
<span data-ttu-id="847a5-235">hello 下列程式碼會示範如何 tooregister hello hello ADO.NET 驅動程式與 Azure 金鑰保存庫提供者。</span><span class="sxs-lookup"><span data-stu-id="847a5-235">hello following code shows how tooregister hello Azure Key Vault provider with hello ADO.NET driver.</span></span>

    private static ClientCredential _clientCredential;

    static void InitializeAzureKeyVaultProvider()
    {
       _clientCredential = new ClientCredential(clientId, clientSecret);

       SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
          new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

       Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
          new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

       providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
       SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
    }



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="847a5-236">一律加密範例主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="847a5-236">Always Encrypted sample console application</span></span>
<span data-ttu-id="847a5-237">這個範例會示範如何：</span><span class="sxs-lookup"><span data-stu-id="847a5-237">This sample demonstrates how to:</span></span>

* <span data-ttu-id="847a5-238">修改您永遠加密的連接字串 tooenable。</span><span class="sxs-lookup"><span data-stu-id="847a5-238">Modify your connection string tooenable Always Encrypted.</span></span>
* <span data-ttu-id="847a5-239">登錄 Azure 金鑰保存庫，因為 hello 應用程式的金鑰存放區提供者。</span><span class="sxs-lookup"><span data-stu-id="847a5-239">Register Azure Key Vault as hello application's key store provider.</span></span>  
* <span data-ttu-id="847a5-240">將資料插入加密的 hello 資料行。</span><span class="sxs-lookup"><span data-stu-id="847a5-240">Insert data into hello encrypted columns.</span></span>
* <span data-ttu-id="847a5-241">在加密資料行中篩選特定值來選取記錄。</span><span class="sxs-lookup"><span data-stu-id="847a5-241">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="847a5-242">取代 hello 內容**Program.cs**以下列程式碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="847a5-242">Replace hello contents of **Program.cs** with hello following code.</span></span> <span data-ttu-id="847a5-243">取代 hello hello 全域 connectionString 中的變數直接位於您從 hello Azure 入口網站的有效的連接字串 hello Main 方法的 hello 列的連接字串。</span><span class="sxs-lookup"><span data-stu-id="847a5-243">Replace hello connection string for hello global connectionString variable in hello line that directly precedes hello Main method with your valid connection string from hello Azure portal.</span></span> <span data-ttu-id="847a5-244">這是 hello 唯一的變更，您需要 toomake toothis 程式碼。</span><span class="sxs-lookup"><span data-stu-id="847a5-244">This is hello only change you need toomake toothis code.</span></span>

<span data-ttu-id="847a5-245">永遠加密的 hello 應用程式 toosee 在中執行動作。</span><span class="sxs-lookup"><span data-stu-id="847a5-245">Run hello app toosee Always Encrypted in action.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider;

    namespace AlwaysEncryptedConsoleAKVApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"<connection string from hello portal>";
        static string clientId = @"<client id from step 7 above>";
        static string clientSecret = "<key from step 13 above>";


        static void Main(string[] args)
        {
            InitializeAzureKeyVaultProvider();

            Console.WriteLine("Signed in as: " + _clientCredential.ClientId);

            Console.WriteLine("Original connection string copied from hello Azure portal:");
            Console.WriteLine(connectionString);

            // Create a SqlConnectionStringBuilder.
            SqlConnectionStringBuilder connStringBuilder =
                new SqlConnectionStringBuilder(connectionString);

            // Enable Always Encrypted for hello connection.
            // This is hello only change specific tooAlways Encrypted
            connStringBuilder.ColumnEncryptionSetting =
                SqlConnectionColumnEncryptionSetting.Enabled;

            Console.WriteLine(Environment.NewLine + "Updated connection string with Always Encrypted enabled:");
            Console.WriteLine(connStringBuilder.ConnectionString);

            // Update hello connection string with a password supplied at runtime.
            Console.WriteLine(Environment.NewLine + "Enter server password:");
            connStringBuilder.Password = Console.ReadLine();


            // Assign hello updated connection string tooour global variable.
            connectionString = connStringBuilder.ConnectionString;


            // Delete all records toorestart this demo app.
            ResetPatientsTable();

            // Add sample data toohello Patients table.
            Console.Write(Environment.NewLine + "Adding sample patient data toohello database...");

            InsertPatient(new Patient()
            {
                SSN = "999-99-0001",
                FirstName = "Orlando",
                LastName = "Gee",
                BirthDate = DateTime.Parse("01/04/1964")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0002",
                FirstName = "Keith",
                LastName = "Harris",
                BirthDate = DateTime.Parse("06/20/1977")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0003",
                FirstName = "Donna",
                LastName = "Carreras",
                BirthDate = DateTime.Parse("02/09/1973")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0004",
                FirstName = "Janet",
                LastName = "Gates",
                BirthDate = DateTime.Parse("08/31/1985")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0005",
                FirstName = "Lucy",
                LastName = "Harrington",
                BirthDate = DateTime.Parse("05/06/1993")
            });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now lets locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 999-99-0003):");
                ssn = Console.ReadLine();
            } while (ssn.Length != 11);

            // hello example allows duplicate SSN entries so we will return all records
            // that match hello provided value and store hello results in selectedPatients.
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

            Console.WriteLine("Press Enter tooexit...");
            Console.ReadLine();
        }


        private static ClientCredential _clientCredential;

        static void InitializeAzureKeyVaultProvider()
        {

            _clientCredential = new ClientCredential(clientId, clientSecret);

            SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
              new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

            Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
              new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

            providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
            SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
        }

        public async static Task<string> GetToken(string authority, string resource, string scope)
        {
            var authContext = new AuthenticationContext(authority);
            AuthenticationResult result = await authContext.AcquireTokenAsync(resource, _clientCredential);

            if (result == null)
                throw new InvalidOperationException("Failed tooobtain hello access token");
            return result.AccessToken;
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
                    Console.WriteLine("hello following error was encountered: ");
                    Console.WriteLine(ex.Message);
                    Console.WriteLine(Environment.NewLine + "Press Enter key tooexit");
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


        // This method simply deletes all records in hello Patients table tooreset our demo.
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



## <a name="verify-that-hello-data-is-encrypted"></a><span data-ttu-id="847a5-246">驗證已加密 hello 資料</span><span class="sxs-lookup"><span data-stu-id="847a5-246">Verify that hello data is encrypted</span></span>
<span data-ttu-id="847a5-247">您可以快速檢查 hello hello 伺服器上的實際資料由查詢使用 SSMS hello 病患資料加密 (使用目前的連接位置**Column Encryption Setting**尚未啟用)。</span><span class="sxs-lookup"><span data-stu-id="847a5-247">You can quickly check that hello actual data on hello server is encrypted by querying hello Patients data with SSMS (using your current connection where **Column Encryption Setting** is not yet enabled).</span></span>

<span data-ttu-id="847a5-248">執行下列查詢 hello 診所資料庫上的 hello。</span><span class="sxs-lookup"><span data-stu-id="847a5-248">Run hello following query on hello Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="847a5-249">您可以看到 hello 加密資料行不包含任何純文字資料。</span><span class="sxs-lookup"><span data-stu-id="847a5-249">You can see that hello encrypted columns do not contain any plaintext data.</span></span>

   ![新的主控台應用程式](./media/sql-database-always-encrypted-azure-key-vault/ssms-encrypted.png)

<span data-ttu-id="847a5-251">toouse SSMS tooaccess hello 純文字資料，您可以加入 hello *Column Encryption Setting = 啟用*參數 toohello 連線。</span><span class="sxs-lookup"><span data-stu-id="847a5-251">toouse SSMS tooaccess hello plaintext data, you can add hello *Column Encryption Setting=enabled* parameter toohello connection.</span></span>

1. <span data-ttu-id="847a5-252">在 SSMS 中，於 [物件總管] 中您的伺服器上按一下滑鼠右鍵，然後選擇 [中斷連線]。</span><span class="sxs-lookup"><span data-stu-id="847a5-252">In SSMS, right-click your server in **Object Explorer** and choose **Disconnect**.</span></span>
2. <span data-ttu-id="847a5-253">按一下**連接** > **Database Engine** tooopen hello**連接 tooServer**視窗，然後按一下**選項**。</span><span class="sxs-lookup"><span data-stu-id="847a5-253">Click **Connect** > **Database Engine** tooopen hello **Connect tooServer** window and click **Options**.</span></span>
3. <span data-ttu-id="847a5-254">按一下 [其他連接參數] 並輸入 **Column Encryption Setting=enabled**。</span><span class="sxs-lookup"><span data-stu-id="847a5-254">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![新的主控台應用程式](./media/sql-database-always-encrypted-azure-key-vault/ssms-connection-parameter.png)
4. <span data-ttu-id="847a5-256">執行下列查詢 hello 診所資料庫上的 hello。</span><span class="sxs-lookup"><span data-stu-id="847a5-256">Run hello following query on hello Clinic database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="847a5-257">您現在可以看到 hello 加密資料行中的 hello 純文字資料。</span><span class="sxs-lookup"><span data-stu-id="847a5-257">You can now see hello plaintext data in hello encrypted columns.</span></span>

    ![新的主控台應用程式](./media/sql-database-always-encrypted-azure-key-vault/ssms-plaintext.png)


## <a name="next-steps"></a><span data-ttu-id="847a5-259">後續步驟</span><span class="sxs-lookup"><span data-stu-id="847a5-259">Next steps</span></span>
<span data-ttu-id="847a5-260">建立使用永遠加密的資料庫之後，您可能想 toodo hello 下列：</span><span class="sxs-lookup"><span data-stu-id="847a5-260">After you create a database that uses Always Encrypted, you may want toodo hello following:</span></span>

* <span data-ttu-id="847a5-261">[輪替和清除金鑰](https://msdn.microsoft.com/library/mt607048.aspx)。</span><span class="sxs-lookup"><span data-stu-id="847a5-261">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="847a5-262">[移轉已經透過一律加密來加密的資料](https://msdn.microsoft.com/library/mt621539.aspx)。</span><span class="sxs-lookup"><span data-stu-id="847a5-262">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>

## <a name="related-information"></a><span data-ttu-id="847a5-263">相關資訊</span><span class="sxs-lookup"><span data-stu-id="847a5-263">Related information</span></span>
* [<span data-ttu-id="847a5-264">一律加密 (用戶端開發)</span><span class="sxs-lookup"><span data-stu-id="847a5-264">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="847a5-265">透明資料加密</span><span class="sxs-lookup"><span data-stu-id="847a5-265">Transparent data encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="847a5-266">SQL Server 加密</span><span class="sxs-lookup"><span data-stu-id="847a5-266">SQL Server encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="847a5-267">一律加密精靈</span><span class="sxs-lookup"><span data-stu-id="847a5-267">Always Encrypted wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="847a5-268">一律加密部落格</span><span class="sxs-lookup"><span data-stu-id="847a5-268">Always Encrypted blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

