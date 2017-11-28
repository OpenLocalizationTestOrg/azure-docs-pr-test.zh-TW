---
title: "永遠加密：SQL Database - Azure Key Vault | Microsoft Docs"
description: "本文說明如何使用 SQL Server Management Studio 中的 [永遠加密精靈]，藉由資料加密來保護 SQL Database 中的機密資料。 它也包含示範如何將每個加密金鑰儲存在「Azure 金鑰保存庫」中的指示。"
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
ms.openlocfilehash: 61bfd420425b4740f6d4ebc01a403a88ff351382
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-azure-key-vault"></a><span data-ttu-id="6d120-105">一律加密：保護 SQL Database 中的機密資料，並將加密金鑰儲存在「Azure 金鑰保存庫」中</span><span class="sxs-lookup"><span data-stu-id="6d120-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in Azure Key Vault</span></span>

<span data-ttu-id="6d120-106">本文說明如何使用 [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx) 中的[一律加密精靈](https://msdn.microsoft.com/library/mt459280.aspx)，藉由資料加密來保護 SQL Database 中的機密資料。</span><span class="sxs-lookup"><span data-stu-id="6d120-106">This article shows you how to secure sensitive data in a SQL database with data encryption using the [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="6d120-107">它也包含示範如何將每個加密金鑰儲存在「Azure 金鑰保存庫」中的指示。</span><span class="sxs-lookup"><span data-stu-id="6d120-107">It also includes instructions that will show you how to store each encryption key in Azure Key Vault.</span></span>

<span data-ttu-id="6d120-108">「一律加密」是 Azure SQL Database 和 SQL Server 中新的資料加密技術，不論是當機密資料在伺服器上待用時、在用戶端與伺服器之間移動時，還是使用中時，都可協助保護資料。</span><span class="sxs-lookup"><span data-stu-id="6d120-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on the server, during movement between client and server, and while the data is in use.</span></span> <span data-ttu-id="6d120-109">「一律加密」可確保機密資料在資料庫系統內一律不會以純文字顯示。</span><span class="sxs-lookup"><span data-stu-id="6d120-109">Always Encrypted ensures that sensitive data never appears as plaintext inside the database system.</span></span> <span data-ttu-id="6d120-110">設定資料加密之後，只有具備金鑰存取權的用戶端應用程式或應用程式伺服器才可以存取純文字資料。</span><span class="sxs-lookup"><span data-stu-id="6d120-110">After you configure data encryption, only client applications or app servers that have access to the keys can access plaintext data.</span></span> <span data-ttu-id="6d120-111">如需詳細資訊，請參閱 [一律加密 (資料庫引擎)](https://msdn.microsoft.com/library/mt163865.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6d120-111">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="6d120-112">將資料庫設定為使用「一律加密」之後，您將使用 Visual Studio 以 C# 建立用戶端應用程式來使用加密資料。</span><span class="sxs-lookup"><span data-stu-id="6d120-112">After you configure the database to use Always Encrypted, you will create a client application in C# with Visual Studio to work with the encrypted data.</span></span>

<span data-ttu-id="6d120-113">請依照本文章中的步驟操作，並了解如何為 Azure SQL Database 設定「一律加密」。</span><span class="sxs-lookup"><span data-stu-id="6d120-113">Follow the steps in this article and learn how to set up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="6d120-114">在本文章中，您將學習到如何執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="6d120-114">In this article you will learn how to perform the following tasks:</span></span>

* <span data-ttu-id="6d120-115">使用 SSMS 中的「一律加密」精靈來建立 [一律加密的金鑰](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3)。</span><span class="sxs-lookup"><span data-stu-id="6d120-115">Use the Always Encrypted wizard in SSMS to create [Always Encrypted keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="6d120-116">建立 [資料行主要金鑰 (CMK)](https://msdn.microsoft.com/library/mt146393.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6d120-116">Create a [column master key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="6d120-117">建立 [資料行加密金鑰 (CEK)](https://msdn.microsoft.com/library/mt146372.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6d120-117">Create a [column encryption key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="6d120-118">建立資料庫資料表並將資料行加密。</span><span class="sxs-lookup"><span data-stu-id="6d120-118">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="6d120-119">建立可插入、選取及顯示加密資料行資料的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6d120-119">Create an application that inserts, selects, and displays data from the encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d120-120">必要條件</span><span class="sxs-lookup"><span data-stu-id="6d120-120">Prerequisites</span></span>
<span data-ttu-id="6d120-121">針對本教學課程，您將需要：</span><span class="sxs-lookup"><span data-stu-id="6d120-121">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="6d120-122">Azure 帳戶和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6d120-122">An Azure account and subscription.</span></span> <span data-ttu-id="6d120-123">如果您沒有帳戶，請註冊 [免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="6d120-123">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="6d120-124">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 13.0.700.242 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6d120-124">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="6d120-125">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) 或更新版本 (於用戶端電腦上)。</span><span class="sxs-lookup"><span data-stu-id="6d120-125">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on the client computer).</span></span>
* <span data-ttu-id="6d120-126">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6d120-126">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>
* <span data-ttu-id="6d120-127">[Azure PowerShell](/powershell/azure/overview) 1.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6d120-127">[Azure PowerShell](/powershell/azure/overview), version  1.0 or later.</span></span> <span data-ttu-id="6d120-128">請輸入 **(Get-Module azure -ListAvailable).Version** 來查看您正在執行的 PowerShell 版本。</span><span class="sxs-lookup"><span data-stu-id="6d120-128">Type **(Get-Module azure -ListAvailable).Version** to see what version of PowerShell you are running.</span></span>

## <a name="enable-your-client-application-to-access-the-sql-database-service"></a><span data-ttu-id="6d120-129">讓用戶端應用程式能夠存取 SQL Database 服務</span><span class="sxs-lookup"><span data-stu-id="6d120-129">Enable your client application to access the SQL Database service</span></span>
<span data-ttu-id="6d120-130">您必須讓用戶端應用程式能夠存取 SQL Database 服務，方法是設定必要的驗證，並取得在接下來的程式碼中驗證應用程式所需的「用戶端識別碼」和「密碼」。</span><span class="sxs-lookup"><span data-stu-id="6d120-130">You must enable your client application to access the SQL Database service by setting up the required authentication and acquiring the *ClientId* and *Secret* that you will need to authenticate your application in the following code.</span></span>

1. <span data-ttu-id="6d120-131">開啟 [Azure 傳統入口網站](http://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="6d120-131">Open the [Azure classic portal](http://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="6d120-132">選取 [Active Directory]  ，然後按一下您應用程式將會使用的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="6d120-132">Select **Active Directory** and click the Active Directory instance that your application will use.</span></span>
3. <span data-ttu-id="6d120-133">按一下 [應用程式]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="6d120-133">Click **Applications**, and then click **ADD**.</span></span>
4. <span data-ttu-id="6d120-134">輸入您應用程式的名稱 (例如：*myClientApp*)，選取 [WEB 應用程式]，然後按一下箭號以繼續。</span><span class="sxs-lookup"><span data-stu-id="6d120-134">Type a name for your application (for example: *myClientApp*), select **WEB APPLICATION**, and click the arrow to continue.</span></span>
5. <span data-ttu-id="6d120-135">針對 [登入 URL] 和 [應用程式識別碼 URI]，您可以輸入一個有效的 URL (例如： *http://myClientApp* )，然後繼續。</span><span class="sxs-lookup"><span data-stu-id="6d120-135">For the **SIGN-ON URL** and **APP ID URI** you can type a valid URL (for example, *http://myClientApp*) and continue.</span></span>
6. <span data-ttu-id="6d120-136">按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="6d120-136">Click **CONFIGURE**.</span></span>
7. <span data-ttu-id="6d120-137">複製您的 [用戶端識別碼] 。</span><span class="sxs-lookup"><span data-stu-id="6d120-137">Copy your **CLIENT ID**.</span></span> <span data-ttu-id="6d120-138">(您之後在程式碼中將需要此值)。</span><span class="sxs-lookup"><span data-stu-id="6d120-138">(You will need this value in your code later.)</span></span>
8. <span data-ttu-id="6d120-139">在 [金鑰] 區段中，從 [選取持續時間] 下拉式清單中選取 [1 年]。</span><span class="sxs-lookup"><span data-stu-id="6d120-139">In the **keys** section, select **1 year** from the  **Select duration** drop-down list.</span></span> <span data-ttu-id="6d120-140">(您將在儲存金鑰後，於步驟 13 複製金鑰)。</span><span class="sxs-lookup"><span data-stu-id="6d120-140">(You will copy the key after you save in step 13.)</span></span>
9. <span data-ttu-id="6d120-141">向下捲動並按一下 [新增應用程式] 。</span><span class="sxs-lookup"><span data-stu-id="6d120-141">Scroll down and click **Add application**.</span></span>
10. <span data-ttu-id="6d120-142">將 [顯示] 保留設定為 [Microsoft 應用程式]，然後選取 [Microsoft Azure 服務管理 API]。</span><span class="sxs-lookup"><span data-stu-id="6d120-142">Leave **SHOW** set to **Microsoft Apps** and select **Microsoft Azure Service Management API**.</span></span> <span data-ttu-id="6d120-143">按一下核取記號以繼續。</span><span class="sxs-lookup"><span data-stu-id="6d120-143">Click the checkmark to continue.</span></span>
11. <span data-ttu-id="6d120-144">從 [委派權限] 下拉式清單中選取 [存取 Azure 服務管理...]。</span><span class="sxs-lookup"><span data-stu-id="6d120-144">Select **Access Azure Service Management...** from the **Delegated Permissions** drop-down list.</span></span>
12. <span data-ttu-id="6d120-145">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="6d120-145">Click **SAVE**.</span></span>
13. <span data-ttu-id="6d120-146">完成儲存之後，複製 [金鑰]  區段中的金鑰值。</span><span class="sxs-lookup"><span data-stu-id="6d120-146">After the save finishes, copy the key value in the **keys** section.</span></span> <span data-ttu-id="6d120-147">(您之後在程式碼中將需要此值)。</span><span class="sxs-lookup"><span data-stu-id="6d120-147">(You will need this value in your code later.)</span></span>

## <a name="create-a-key-vault-to-store-your-keys"></a><span data-ttu-id="6d120-148">建立金鑰保存庫來儲存您的金鑰</span><span class="sxs-lookup"><span data-stu-id="6d120-148">Create a key vault to store your keys</span></span>
<span data-ttu-id="6d120-149">既然您的用戶端應用程式已完成設定，您也已取得用戶端識別碼，現在即可建立金鑰保存庫並設定其存取原則，以便讓您和您的應用程式能夠存取保存庫的密碼 (「一律加密」金鑰)。</span><span class="sxs-lookup"><span data-stu-id="6d120-149">Now that your client app is configured and you have your client ID, it's time to create a key vault and configure its access policy so you and your application can access the vault's secrets (the Always Encrypted keys).</span></span> <span data-ttu-id="6d120-150">若要使用 SQL Server Management Studio 來建立新的資料行主要金鑰及設定加密，必須要有 create、get、list、sign、verify、wrapKey 及 unwrapKey 權限。</span><span class="sxs-lookup"><span data-stu-id="6d120-150">The *create*, *get*, *list*, *sign*, *verify*, *wrapKey*, and *unwrapKey* permissions are required for creating a new column master key and for setting up encryption with SQL Server Management Studio.</span></span>

<span data-ttu-id="6d120-151">您可以執行下列指令碼來快速建立金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="6d120-151">You can quickly create a key vault by running the following script.</span></span> <span data-ttu-id="6d120-152">如需這些 Cmdlet 的詳細說明，以及有關建立及設定金鑰保存庫的詳細資訊，請參閱[開始使用 Azure 金鑰保存庫](../key-vault/key-vault-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="6d120-152">For a detailed explanation of these cmdlets and more information about creating and configuring a key vault, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>

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




## <a name="create-a-blank-sql-database"></a><span data-ttu-id="6d120-153">建立空白 SQL Database</span><span class="sxs-lookup"><span data-stu-id="6d120-153">Create a blank SQL database</span></span>
1. <span data-ttu-id="6d120-154">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="6d120-154">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6d120-155">移至 [新增]  >  [資料 + 儲存體]  >  [SQL Database]。</span><span class="sxs-lookup"><span data-stu-id="6d120-155">Go to **New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="6d120-156">在新的或現有伺服器上建立名稱為 **Clinic** (診所) 的**空白**資料庫。</span><span class="sxs-lookup"><span data-stu-id="6d120-156">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="6d120-157">如需有關如何在 Azure 入口網站中建立資料庫的詳細指示，請參閱[您的第一個 SQL Database](sql-database-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="6d120-157">For detailed directions about how to create a database in the Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![建立空白資料庫](./media/sql-database-always-encrypted-azure-key-vault/create-database.png)

<span data-ttu-id="6d120-159">在本教學課程稍後，您將會需要連接字串，因此在建立資料庫之後，請瀏覽至新的 Clinic 資料庫並複製連接字串。</span><span class="sxs-lookup"><span data-stu-id="6d120-159">You will need the connection string later in the tutorial, so after you create the database, browse to the new  Clinic database and copy the connection string.</span></span> <span data-ttu-id="6d120-160">您可以隨時取得連接字串，但在 Azure 入口網站中很容易就可以複製它。</span><span class="sxs-lookup"><span data-stu-id="6d120-160">You can get the connection string at any time, but it's easy to copy it in the Azure portal.</span></span>

1. <span data-ttu-id="6d120-161">移至 [SQL Database]  >  [Clinic]  >  [顯示資料庫連接字串]。</span><span class="sxs-lookup"><span data-stu-id="6d120-161">Go to **SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="6d120-162">複製 **ADO.NET**的連接字串。</span><span class="sxs-lookup"><span data-stu-id="6d120-162">Copy the connection string for **ADO.NET**.</span></span>
   
    ![複製連接字串](./media/sql-database-always-encrypted-azure-key-vault/connection-strings.png)

## <a name="connect-to-the-database-with-ssms"></a><span data-ttu-id="6d120-164">使用 SSMS 連接到資料庫</span><span class="sxs-lookup"><span data-stu-id="6d120-164">Connect to the database with SSMS</span></span>
<span data-ttu-id="6d120-165">開啟 SSMS 並連接到包含實務課程資料庫的伺服器。</span><span class="sxs-lookup"><span data-stu-id="6d120-165">Open SSMS and connect to the server with the Clinic database.</span></span>

1. <span data-ttu-id="6d120-166">開啟 SSMS。</span><span class="sxs-lookup"><span data-stu-id="6d120-166">Open SSMS.</span></span> <span data-ttu-id="6d120-167">(移至 [連接]  >  [資料庫引擎] 以開啟 [連接到伺服器] 視窗 (如果此視窗未開啟))。</span><span class="sxs-lookup"><span data-stu-id="6d120-167">(Go to **Connect** > **Database Engine** to open the **Connect to Server** window if it isn't open.)</span></span>
2. <span data-ttu-id="6d120-168">輸入您的伺服器名稱和認證。</span><span class="sxs-lookup"><span data-stu-id="6d120-168">Enter your server name and credentials.</span></span> <span data-ttu-id="6d120-169">可以在 SQL 資料庫刀鋒視窗上找到此伺服器名稱和稍早複製的連接字串。</span><span class="sxs-lookup"><span data-stu-id="6d120-169">The server name can be found on the SQL database blade and in the connection string you copied earlier.</span></span> <span data-ttu-id="6d120-170">輸入完整的伺服器名稱，包括 *database.windows.net*。</span><span class="sxs-lookup"><span data-stu-id="6d120-170">Type the complete server name, including *database.windows.net*.</span></span>
   
    ![複製連接字串](./media/sql-database-always-encrypted-azure-key-vault/ssms-connect.png)

<span data-ttu-id="6d120-172">如果 [新增防火牆規則]  視窗開啟，請登入 Azure，讓 SSMS 為您建立新的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="6d120-172">If the **New Firewall Rule** window opens, sign in to Azure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="6d120-173">建立資料表</span><span class="sxs-lookup"><span data-stu-id="6d120-173">Create a table</span></span>
<span data-ttu-id="6d120-174">在本節中，您將建立資料表來保存病患的資料。</span><span class="sxs-lookup"><span data-stu-id="6d120-174">In this section, you will create a table to hold patient data.</span></span> <span data-ttu-id="6d120-175">它一開始並未加密 -- 您將在下一節中設定加密。</span><span class="sxs-lookup"><span data-stu-id="6d120-175">It's not initially encrypted--you will configure encryption in the next section.</span></span>

1. <span data-ttu-id="6d120-176">展開 [資料庫] 。</span><span class="sxs-lookup"><span data-stu-id="6d120-176">Expand **Databases**.</span></span>
2. <span data-ttu-id="6d120-177">在 [Clinic] 資料庫上按一下滑鼠右鍵，然後按一下 [新增查詢]。</span><span class="sxs-lookup"><span data-stu-id="6d120-177">Right-click the **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="6d120-178">將下列 Transact-SQL (T-SQL) 貼到新的查詢視窗中並「執行」  它。</span><span class="sxs-lookup"><span data-stu-id="6d120-178">Paste the following Transact-SQL (T-SQL) into the new query window and **Execute** it.</span></span>

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


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="6d120-179">將資料行加密 (設定「一律加密」)</span><span class="sxs-lookup"><span data-stu-id="6d120-179">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="6d120-180">SSMS 提供一個精靈，可為您設定資料行主要金鑰、資料行加密金鑰及加密的資料行，來協助您輕鬆設定「一律加密」。</span><span class="sxs-lookup"><span data-stu-id="6d120-180">SSMS provides a wizard that helps you easily configure Always Encrypted by setting up the column master key, column encryption key, and encrypted columns for you.</span></span>

1. <span data-ttu-id="6d120-181">展開 [資料庫]  > **空白** > ，藉由資料庫加密來保護 SQL Database 中的機密資料。</span><span class="sxs-lookup"><span data-stu-id="6d120-181">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="6d120-182">在 [Patients] 資料表上按一下滑鼠右鍵，然後選取 [加密資料行] 以開啟「一律加密精靈」：</span><span class="sxs-lookup"><span data-stu-id="6d120-182">Right-click the **Patients** table and select **Encrypt Columns** to open the Always Encrypted wizard:</span></span>
   
    ![加密資料行](./media/sql-database-always-encrypted-azure-key-vault/encrypt-columns.png)

<span data-ttu-id="6d120-184">「一律加密」精靈包含下列區段︰[資料行選取]、主要金鑰組態、[驗證] 及 [摘要]。</span><span class="sxs-lookup"><span data-stu-id="6d120-184">The Always Encrypted wizard includes the following sections: **Column Selection**, **Master Key Configuration**, **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="6d120-185">資料行選取</span><span class="sxs-lookup"><span data-stu-id="6d120-185">Column Selection</span></span>
<span data-ttu-id="6d120-186">在 [簡介] 頁面上按 [下一步]，即可開啟 [資料行選取] 頁面。</span><span class="sxs-lookup"><span data-stu-id="6d120-186">Click **Next** on the **Introduction** page to open the **Column Selection** page.</span></span> <span data-ttu-id="6d120-187">在此頁面上，您將選取要加密的資料行、 [加密類型及要使用的資料行加密金鑰 (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) 。</span><span class="sxs-lookup"><span data-stu-id="6d120-187">On this page, you will select which columns you want to encrypt, [the type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) to use.</span></span>

<span data-ttu-id="6d120-188">請加密每個病患的 **SSN** 和 **BirthDate** 資訊。</span><span class="sxs-lookup"><span data-stu-id="6d120-188">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="6d120-189">SSN 資料行將使用決定性加密，這可支援等式查閱、聯結及群組依據。</span><span class="sxs-lookup"><span data-stu-id="6d120-189">The SSN column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="6d120-190">BirthDate 資料行將使用不支援操作的隨機加密。</span><span class="sxs-lookup"><span data-stu-id="6d120-190">The BirthDate column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="6d120-191">將 SSN 資料行的 [加密類型] 設定為 [決定性]，並將 BirthDate 資料行設定為 [隨機化]。</span><span class="sxs-lookup"><span data-stu-id="6d120-191">Set the **Encryption Type** for the SSN column to **Deterministic** and the BirthDate column to **Randomized**.</span></span> <span data-ttu-id="6d120-192">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="6d120-192">Click **Next**.</span></span>

![加密資料行](./media/sql-database-always-encrypted-azure-key-vault/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="6d120-194">主要金鑰組態</span><span class="sxs-lookup"><span data-stu-id="6d120-194">Master Key Configuration</span></span>
<span data-ttu-id="6d120-195">您可以在 [主要金鑰組態]  頁面設定 CMK，以及選取要用來儲存 CMK 的金鑰存放區提供者。</span><span class="sxs-lookup"><span data-stu-id="6d120-195">The **Master Key Configuration** page is where you set up your CMK and select the key store provider where the CMK will be stored.</span></span> <span data-ttu-id="6d120-196">目前，您可以將 CMK 儲存在 Windows 憑證存放區、「Azure 金鑰保存庫」或硬體安全性模組 (HSM) 中。</span><span class="sxs-lookup"><span data-stu-id="6d120-196">Currently, you can store a CMK in the Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span>

<span data-ttu-id="6d120-197">本教學課程將說明如何將金鑰儲存在「Azure 金鑰保存庫」中。</span><span class="sxs-lookup"><span data-stu-id="6d120-197">This tutorial shows how to store your keys in Azure Key Vault.</span></span>

1. <span data-ttu-id="6d120-198">選取 [Azure 金鑰保存庫] 。</span><span class="sxs-lookup"><span data-stu-id="6d120-198">Select **Azure Key Vault**.</span></span>
2. <span data-ttu-id="6d120-199">從下拉式清單中選取想要的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="6d120-199">Select the desired key vault from the drop-down list.</span></span>
3. <span data-ttu-id="6d120-200">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="6d120-200">Click **Next**.</span></span>

![主要金鑰組態](./media/sql-database-always-encrypted-azure-key-vault/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="6d120-202">驗證</span><span class="sxs-lookup"><span data-stu-id="6d120-202">Validation</span></span>
<span data-ttu-id="6d120-203">您現在可以加密資料行，或儲存為 PowerShell 指令碼以供日後執行。</span><span class="sxs-lookup"><span data-stu-id="6d120-203">You can encrypt the columns now or save a PowerShell script to run later.</span></span> <span data-ttu-id="6d120-204">針對這個教學課程，請選取 [繼續以立即完成]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="6d120-204">For this tutorial, select **Proceed to finish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="6d120-205">摘要</span><span class="sxs-lookup"><span data-stu-id="6d120-205">Summary</span></span>
<span data-ttu-id="6d120-206">確認設定全都正確，然後按一下 [完成]  以完成 [一律加密] 的設定。</span><span class="sxs-lookup"><span data-stu-id="6d120-206">Verify that the settings are all correct and click **Finish** to complete the setup for Always Encrypted.</span></span>

![摘要](./media/sql-database-always-encrypted-azure-key-vault/summary.png)

### <a name="verify-the-wizards-actions"></a><span data-ttu-id="6d120-208">確認精靈的動作</span><span class="sxs-lookup"><span data-stu-id="6d120-208">Verify the wizard's actions</span></span>
<span data-ttu-id="6d120-209">完成精靈步驟之後，您的資料庫便已完成「一律加密」設定。</span><span class="sxs-lookup"><span data-stu-id="6d120-209">After the wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="6d120-210">精靈已執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="6d120-210">The wizard performed the following actions:</span></span>

* <span data-ttu-id="6d120-211">建立資料行主要金鑰 (CMK) 並將它儲存在「Azure 金鑰保存庫」中。</span><span class="sxs-lookup"><span data-stu-id="6d120-211">Created a column master key and stored it in Azure Key Vault.</span></span>
* <span data-ttu-id="6d120-212">建立資料行加密金鑰 (CMK) 並將它儲存在「Azure 金鑰保存庫」中。</span><span class="sxs-lookup"><span data-stu-id="6d120-212">Created a column encryption key and stored it in Azure Key Vault.</span></span>
* <span data-ttu-id="6d120-213">設定選取的資料行以進行加密。</span><span class="sxs-lookup"><span data-stu-id="6d120-213">Configured the selected columns for encryption.</span></span> <span data-ttu-id="6d120-214">Patients 資料表目前沒有任何資料，但在所選資料行中的所有現有資料現在都已加密。</span><span class="sxs-lookup"><span data-stu-id="6d120-214">The Patients table currently has no data, but any existing data in the selected columns is now encrypted.</span></span>

<span data-ttu-id="6d120-215">您可以確認 SSMS 中是否已建立金鑰，方法是展開 [Clinic]  >  [安全性]  >  [一律加密的金鑰]。</span><span class="sxs-lookup"><span data-stu-id="6d120-215">You can verify the creation of the keys in SSMS by expanding **Clinic** > **Security** > **Always Encrypted Keys**.</span></span>

## <a name="create-a-client-application-that-works-with-the-encrypted-data"></a><span data-ttu-id="6d120-216">建立搭配加密資料使用的用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="6d120-216">Create a client application that works with the encrypted data</span></span>
<span data-ttu-id="6d120-217">既然已設定好「一律加密」，您現在即可建置會在加密資料行上執行「插入」和「選取」動作的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6d120-217">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on the encrypted columns.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="6d120-218">傳送純文字資料至具有 [一律加密] 資料行的伺服器時，您的應用程式必須使用 [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) 物件。</span><span class="sxs-lookup"><span data-stu-id="6d120-218">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data to the server with Always Encrypted columns.</span></span> <span data-ttu-id="6d120-219">在不使用 SqlParameter 物件的情況下傳遞常值會導致例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6d120-219">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="6d120-220">開啟 Visual Studio 並建立新的 C# **主控台應用程式**(Visual Studio 2015 和更早版本) 或**主控台應用程式 (.NET Framework)** (Visual Studio 2017 和更新版本)。</span><span class="sxs-lookup"><span data-stu-id="6d120-220">Open Visual Studio and create a new C# **Console Application** (Visual Studio 2015 and earlier) or **Console App (.NET Framework)** (Visual Studio 2017 and later).</span></span> <span data-ttu-id="6d120-221">請確定您的專案設定為 **.NET Framework 4.6** 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6d120-221">Make sure your project is set to **.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="6d120-222">將專案命名為 **AlwaysEncryptedConsoleAKVApp**，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="6d120-222">Name the project **AlwaysEncryptedConsoleAKVApp** and click **OK**.</span></span>
3. <span data-ttu-id="6d120-223">移至 [工具]  >  [NuGet 套件管理員]  >  [套件管理員主控台]，以安裝下列 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="6d120-223">Install the following NuGet packages by going to **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="6d120-224">在 [封裝管理員主控台] 中執行下列兩行程式碼。</span><span class="sxs-lookup"><span data-stu-id="6d120-224">Run these two lines of code in the Package Manager Console.</span></span>

    Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory



## <a name="modify-your-connection-string-to-enable-always-encrypted"></a><span data-ttu-id="6d120-225">修改連接字串，以啟用 [一律加密]</span><span class="sxs-lookup"><span data-stu-id="6d120-225">Modify your connection string to enable Always Encrypted</span></span>
<span data-ttu-id="6d120-226">本節說明如何在您的資料庫連接字串中啟用「一律加密」。</span><span class="sxs-lookup"><span data-stu-id="6d120-226">This section  explains how to enable Always Encrypted in your database connection string.</span></span>

<span data-ttu-id="6d120-227">若要啟用「一律加密」，您必須將 **Column Encryption Setting** 關鍵字新增到您的連接字串中，並將它設定為 **Enabled**。</span><span class="sxs-lookup"><span data-stu-id="6d120-227">To enable Always Encrypted, you need to add the **Column Encryption Setting** keyword to your connection string and set it to **Enabled**.</span></span>

<span data-ttu-id="6d120-228">您可以直接在連接字串中進行此設定，或是使用 [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx)來設定它。</span><span class="sxs-lookup"><span data-stu-id="6d120-228">You can set this directly in the connection string, or you can set it by using [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="6d120-229">下一節中的範例應用程式會示範如何使用 **SqlConnectionStringBuilder**。</span><span class="sxs-lookup"><span data-stu-id="6d120-229">The sample application in the next section shows how to use **SqlConnectionStringBuilder**.</span></span>

### <a name="enable-always-encrypted-in-the-connection-string"></a><span data-ttu-id="6d120-230">在連接字串中啟用 [一律加密]</span><span class="sxs-lookup"><span data-stu-id="6d120-230">Enable Always Encrypted in the connection string</span></span>
<span data-ttu-id="6d120-231">在連接字串中加入下列關鍵字。</span><span class="sxs-lookup"><span data-stu-id="6d120-231">Add the following keyword to your connection string.</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-sqlconnectionstringbuilder"></a><span data-ttu-id="6d120-232">使用 SqlConnectionStringBuilder 來啟用一律加密</span><span class="sxs-lookup"><span data-stu-id="6d120-232">Enable Always Encrypted with SqlConnectionStringBuilder</span></span>
<span data-ttu-id="6d120-233">下列程式碼示範如何將 [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) 設定為 [Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx) 來啟用「一律加密」。</span><span class="sxs-lookup"><span data-stu-id="6d120-233">The following code shows how to enable Always Encrypted by setting [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) to [Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;

## <a name="register-the-azure-key-vault-provider"></a><span data-ttu-id="6d120-234">註冊 Azure 金鑰保存庫提供者</span><span class="sxs-lookup"><span data-stu-id="6d120-234">Register the Azure Key Vault provider</span></span>
<span data-ttu-id="6d120-235">下列程式碼示範如何使用 ADO.NET 驅動程式來註冊「Azure 金鑰保存庫」提供者。</span><span class="sxs-lookup"><span data-stu-id="6d120-235">The following code shows how to register the Azure Key Vault provider with the ADO.NET driver.</span></span>

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



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="6d120-236">一律加密範例主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="6d120-236">Always Encrypted sample console application</span></span>
<span data-ttu-id="6d120-237">這個範例會示範如何：</span><span class="sxs-lookup"><span data-stu-id="6d120-237">This sample demonstrates how to:</span></span>

* <span data-ttu-id="6d120-238">修改連接字串，以啟用 [一律加密]。</span><span class="sxs-lookup"><span data-stu-id="6d120-238">Modify your connection string to enable Always Encrypted.</span></span>
* <span data-ttu-id="6d120-239">將「Azure 金鑰保存庫」註冊為應用程式的金鑰存放區提供者。</span><span class="sxs-lookup"><span data-stu-id="6d120-239">Register Azure Key Vault as the application's key store provider.</span></span>  
* <span data-ttu-id="6d120-240">將資料插入加密資料行。</span><span class="sxs-lookup"><span data-stu-id="6d120-240">Insert data into the encrypted columns.</span></span>
* <span data-ttu-id="6d120-241">在加密資料行中篩選特定值來選取記錄。</span><span class="sxs-lookup"><span data-stu-id="6d120-241">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="6d120-242">以下列程式碼取代 **Program.cs** 的內容。</span><span class="sxs-lookup"><span data-stu-id="6d120-242">Replace the contents of **Program.cs** with the following code.</span></span> <span data-ttu-id="6d120-243">從 Azure 入口網站，針對 Main 方法前一行中的全域 connectionString 變數，使用有效的連接字串來取代其連接字串。</span><span class="sxs-lookup"><span data-stu-id="6d120-243">Replace the connection string for the global connectionString variable in the line that directly precedes the Main method with your valid connection string from the Azure portal.</span></span> <span data-ttu-id="6d120-244">這是此程式碼唯一需要進行的變更。</span><span class="sxs-lookup"><span data-stu-id="6d120-244">This is the only change you need to make to this code.</span></span>

<span data-ttu-id="6d120-245">執行應用程式以查看「一律加密」的運作情況。</span><span class="sxs-lookup"><span data-stu-id="6d120-245">Run the app to see Always Encrypted in action.</span></span>

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
        // Update this line with your Clinic database connection string from the Azure portal.
        static string connectionString = @"<connection string from the portal>";
        static string clientId = @"<client id from step 7 above>";
        static string clientSecret = "<key from step 13 above>";


        static void Main(string[] args)
        {
            InitializeAzureKeyVaultProvider();

            Console.WriteLine("Signed in as: " + _clientCredential.ClientId);

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
            Console.WriteLine(Environment.NewLine + "All the records currently in the Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now lets locate records by searching the encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that the user entered 11 characters.
            // In production be sure to check all user input and use the best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 999-99-0003):");
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
                throw new InvalidOperationException("Failed to obtain the access token");
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



## <a name="verify-that-the-data-is-encrypted"></a><span data-ttu-id="6d120-246">確認資料已加密</span><span class="sxs-lookup"><span data-stu-id="6d120-246">Verify that the data is encrypted</span></span>
<span data-ttu-id="6d120-247">您可以透過使用 SSMS 來查詢 Patients 資料 (使用尚未啟用「資料行加密設定」  的目前連線)，快速檢查伺服器上的實際資料是否已加密。</span><span class="sxs-lookup"><span data-stu-id="6d120-247">You can quickly check that the actual data on the server is encrypted by querying the Patients data with SSMS (using your current connection where **Column Encryption Setting** is not yet enabled).</span></span>

<span data-ttu-id="6d120-248">在 Clinic 資料庫上執行下列查詢。</span><span class="sxs-lookup"><span data-stu-id="6d120-248">Run the following query on the Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="6d120-249">您可以看到加密的資料行不包含任何純文字資料。</span><span class="sxs-lookup"><span data-stu-id="6d120-249">You can see that the encrypted columns do not contain any plaintext data.</span></span>

   ![新的主控台應用程式](./media/sql-database-always-encrypted-azure-key-vault/ssms-encrypted.png)

<span data-ttu-id="6d120-251">若要使用 SSMS 來存取純文字資料，您可以將 *Column Encryption Setting=enabled* 參數新增到連線中。</span><span class="sxs-lookup"><span data-stu-id="6d120-251">To use SSMS to access the plaintext data, you can add the *Column Encryption Setting=enabled* parameter to the connection.</span></span>

1. <span data-ttu-id="6d120-252">在 SSMS 中，於 [物件總管] 中您的伺服器上按一下滑鼠右鍵，然後選擇 [中斷連線]。</span><span class="sxs-lookup"><span data-stu-id="6d120-252">In SSMS, right-click your server in **Object Explorer** and choose **Disconnect**.</span></span>
2. <span data-ttu-id="6d120-253">按一下 [連接]  >  [資料庫引擎] 以開啟 [連接到伺服器] 視窗，然後按一下 [選項]。</span><span class="sxs-lookup"><span data-stu-id="6d120-253">Click **Connect** > **Database Engine** to open the **Connect to Server** window and click **Options**.</span></span>
3. <span data-ttu-id="6d120-254">按一下 [其他連接參數] 並輸入 **Column Encryption Setting=enabled**。</span><span class="sxs-lookup"><span data-stu-id="6d120-254">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![新的主控台應用程式](./media/sql-database-always-encrypted-azure-key-vault/ssms-connection-parameter.png)
4. <span data-ttu-id="6d120-256">在 Clinic 資料庫上執行下列查詢。</span><span class="sxs-lookup"><span data-stu-id="6d120-256">Run the following query on the Clinic database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="6d120-257">您現在可以在加密的資料行中看到純文字資料。</span><span class="sxs-lookup"><span data-stu-id="6d120-257">You can now see the plaintext data in the encrypted columns.</span></span>

    ![新的主控台應用程式](./media/sql-database-always-encrypted-azure-key-vault/ssms-plaintext.png)


## <a name="next-steps"></a><span data-ttu-id="6d120-259">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6d120-259">Next steps</span></span>
<span data-ttu-id="6d120-260">建立使用「一律加密」的資料庫之後，您可以執行下列操作：</span><span class="sxs-lookup"><span data-stu-id="6d120-260">After you create a database that uses Always Encrypted, you may want to do the following:</span></span>

* <span data-ttu-id="6d120-261">[輪替和清除金鑰](https://msdn.microsoft.com/library/mt607048.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6d120-261">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="6d120-262">[移轉已經透過一律加密來加密的資料](https://msdn.microsoft.com/library/mt621539.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6d120-262">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>

## <a name="related-information"></a><span data-ttu-id="6d120-263">相關資訊</span><span class="sxs-lookup"><span data-stu-id="6d120-263">Related information</span></span>
* [<span data-ttu-id="6d120-264">一律加密 (用戶端開發)</span><span class="sxs-lookup"><span data-stu-id="6d120-264">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="6d120-265">透明資料加密</span><span class="sxs-lookup"><span data-stu-id="6d120-265">Transparent data encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="6d120-266">SQL Server 加密</span><span class="sxs-lookup"><span data-stu-id="6d120-266">SQL Server encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="6d120-267">一律加密精靈</span><span class="sxs-lookup"><span data-stu-id="6d120-267">Always Encrypted wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="6d120-268">一律加密部落格</span><span class="sxs-lookup"><span data-stu-id="6d120-268">Always Encrypted blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

