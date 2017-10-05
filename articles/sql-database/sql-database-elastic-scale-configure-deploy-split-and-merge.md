---
title: "部署分割合併服務 | Microsoft Docs"
description: "使用彈性資料庫工具來分割及合併"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 9a993c0f-7052-46cd-aa59-073bea8d535a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 6e2fea882c248fa095a9d450ed54a7b4e64b45e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-split-merge-service"></a><span data-ttu-id="6a94b-103">部署分割合併服務</span><span class="sxs-lookup"><span data-stu-id="6a94b-103">Deploy a split-merge service</span></span>
<span data-ttu-id="6a94b-104">分割合併工具可讓您在分區化資料庫之間移動資料。</span><span class="sxs-lookup"><span data-stu-id="6a94b-104">The split-merge tool lets you move data between sharded databases.</span></span> <span data-ttu-id="6a94b-105">請參閱 [在相應放大的雲端資料庫之間移動資料](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="6a94b-105">See [Moving data between scaled-out cloud databases](sql-database-elastic-scale-overview-split-and-merge.md)</span></span>

## <a name="download-the-split-merge-packages"></a><span data-ttu-id="6a94b-106">下載分割合併套件</span><span class="sxs-lookup"><span data-stu-id="6a94b-106">Download the Split-Merge packages</span></span>
1. <span data-ttu-id="6a94b-107">從 [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget)下載最新的 NuGet 版本。</span><span class="sxs-lookup"><span data-stu-id="6a94b-107">Download the latest NuGet version from [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span></span>
2. <span data-ttu-id="6a94b-108">開啟命令提示字元並瀏覽至您下載 nuget.exe 的目錄。</span><span class="sxs-lookup"><span data-stu-id="6a94b-108">Open a command prompt and navigate to the directory where you downloaded nuget.exe.</span></span> <span data-ttu-id="6a94b-109">下載包含 PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="6a94b-109">The download includes PowerShell commmands.</span></span>
3. <span data-ttu-id="6a94b-110">使用下列命令，將最新的分割合併封裝下載到目前的目錄：</span><span class="sxs-lookup"><span data-stu-id="6a94b-110">Download the latest Split-Merge package into the current directory with the below command:</span></span>
   ```
   nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge
   ```  

<span data-ttu-id="6a94b-111">檔案會放在名為 **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** 的目錄中，其中 *x.x.xxx.x* 反映版本號碼。</span><span class="sxs-lookup"><span data-stu-id="6a94b-111">The files are placed in a directory named **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** where *x.x.xxx.x* reflects the version number.</span></span> <span data-ttu-id="6a94b-112">在 **content\splitmerge\service** 子目錄中找出分割合併服務檔案，在 **content\splitmerge\powershell** 子目錄中找出分割合併 PowerShell 指令碼 (和必要的用戶端 .dll 檔)。</span><span class="sxs-lookup"><span data-stu-id="6a94b-112">Find the split-merge Service files in the **content\splitmerge\service** sub-directory, and the Split-Merge PowerShell scripts (and required client .dlls) in the **content\splitmerge\powershell** sub-directory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a94b-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="6a94b-113">Prerequisites</span></span>
1. <span data-ttu-id="6a94b-114">建立用來作為分割合併狀態資料庫的 Azure SQL DB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="6a94b-114">Create an Azure SQL DB database that will be used as the split-merge status database.</span></span> <span data-ttu-id="6a94b-115">移至 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="6a94b-115">Go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6a94b-116">建立新的 **SQL Database**。</span><span class="sxs-lookup"><span data-stu-id="6a94b-116">Create a new **SQL Database**.</span></span> <span data-ttu-id="6a94b-117">提供資料庫名稱，並建立新的系統管理員和密碼。</span><span class="sxs-lookup"><span data-stu-id="6a94b-117">Give the database a name and create a new administrator and password.</span></span> <span data-ttu-id="6a94b-118">請務必記錄名稱和密碼，以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="6a94b-118">Be sure to record the name and password for later use.</span></span>
2. <span data-ttu-id="6a94b-119">請確定您的 Azure SQL DB 伺服器允許 Azure 服務進行連接。</span><span class="sxs-lookup"><span data-stu-id="6a94b-119">Ensure that your Azure SQL DB server allows Azure Services to connect to it.</span></span> <span data-ttu-id="6a94b-120">在**防火牆設定**的入口網站中，確定 [允許存取 Azure 服務] 設定設為 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="6a94b-120">In the portal, in the **Firewall Settings**, ensure that the **Allow access to Azure Services** setting is set to **On**.</span></span> <span data-ttu-id="6a94b-121">按一下儲存圖示。</span><span class="sxs-lookup"><span data-stu-id="6a94b-121">Click the "save" icon.</span></span>
   
   ![允許的服務][1]
3. <span data-ttu-id="6a94b-123">建立要用於診斷輸出的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6a94b-123">Create an Azure Storage account that will be used for diagnostics output.</span></span> <span data-ttu-id="6a94b-124">移至 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="6a94b-124">Go to the Azure Portal.</span></span> <span data-ttu-id="6a94b-125">在左列中，按一下 [新增]，按一下 [資料 + 儲存體]，然後按一下 [儲存體]。</span><span class="sxs-lookup"><span data-stu-id="6a94b-125">In the left bar, click **New**, click **Data + Storage**, then **Storage**.</span></span>
4. <span data-ttu-id="6a94b-126">建立將包含分割合併服務的 Azure 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="6a94b-126">Create an Azure Cloud Service that will contain your Split-Merge service.</span></span>  <span data-ttu-id="6a94b-127">移至 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="6a94b-127">Go to the Azure Portal.</span></span> <span data-ttu-id="6a94b-128">在左列中，按一下 [新增]，然後按一下 [計算]、[雲端服務] 和 [建立]。</span><span class="sxs-lookup"><span data-stu-id="6a94b-128">In the left bar, click **New**, then **Compute**, **Cloud Service**, and **Create**.</span></span> 

## <a name="configure-your-split-merge-service"></a><span data-ttu-id="6a94b-129">設定分割合併服務</span><span class="sxs-lookup"><span data-stu-id="6a94b-129">Configure your Split-Merge service</span></span>
### <a name="split-merge-service-configuration"></a><span data-ttu-id="6a94b-130">分割合併服務組態</span><span class="sxs-lookup"><span data-stu-id="6a94b-130">Split-Merge service configuration</span></span>
1. <span data-ttu-id="6a94b-131">在您下載分割合併組件的資料夾中，建立 **ServiceConfiguration.Template.cscfg** 檔案 (隨 **SplitMergeService.cspkg** 一起提供) 的複本，然後重新命名為 **ServiceConfiguration.cscfg**。</span><span class="sxs-lookup"><span data-stu-id="6a94b-131">In the folder where you downloaded the Split-Merge assemblies, create a copy of the **ServiceConfiguration.Template.cscfg** file that shipped alongside **SplitMergeService.cspkg** and rename it **ServiceConfiguration.cscfg**.</span></span>
2. <span data-ttu-id="6a94b-132">在文字編輯器中開啟 **ServiceConfiguration.cscfg** ，例如：會驗證憑證指紋格式等輸入的 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="6a94b-132">Open **ServiceConfiguration.cscfg** in a text editor such as Visual Studio that validates inputs such as the format of certificate thumbprints.</span></span>
3. <span data-ttu-id="6a94b-133">建立新的資料庫或選擇現有的資料庫，做為分割合併作業的狀態資料庫，並擷取該資料庫的連接字串。</span><span class="sxs-lookup"><span data-stu-id="6a94b-133">Create a new database or choose an existing database to serve as the status database for Split-Merge operations and retrieve the connection string of that database.</span></span> 
   
   > [!IMPORTANT]
   > <span data-ttu-id="6a94b-134">目前，狀態資料庫必須使用拉丁文定序 (SQL\_Latin1\_General\_CP1\_CI\_AS)。</span><span class="sxs-lookup"><span data-stu-id="6a94b-134">At this time, the status database must use the Latin  collation (SQL\_Latin1\_General\_CP1\_CI\_AS).</span></span> <span data-ttu-id="6a94b-135">如需詳細資訊，請參閱 [Windows 定序名稱 (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6a94b-135">For more information, see [Windows Collation Name (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span></span>
   >

   <span data-ttu-id="6a94b-136">在 Azure SQL DB 中，連接字串的格式通常為：</span><span class="sxs-lookup"><span data-stu-id="6a94b-136">With Azure SQL DB, the connection string typically is of the form:</span></span>
      ```
      Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
      ```

4. <span data-ttu-id="6a94b-137">在 cscfg 檔案中，在 ElasticScaleMetadata 設定的 **SplitMergeWeb** 和 **SplitMergeWorker** 角色區段中，輸入此連接字串。</span><span class="sxs-lookup"><span data-stu-id="6a94b-137">Enter this connection string in the cscfg file in both the **SplitMergeWeb** and **SplitMergeWorker** role sections in the ElasticScaleMetadata setting.</span></span>
5. <span data-ttu-id="6a94b-138">針對 **SplitMergeWorker** 角色，在 **WorkerRoleSynchronizationStorageAccountConnectionString** 設定中輸入有效的連接字串以連接至 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="6a94b-138">For the **SplitMergeWorker** role, enter a valid connection string to Azure storage for the **WorkerRoleSynchronizationStorageAccountConnectionString** setting.</span></span>

### <a name="configure-security"></a><span data-ttu-id="6a94b-139">設定安全性</span><span class="sxs-lookup"><span data-stu-id="6a94b-139">Configure security</span></span>
<span data-ttu-id="6a94b-140">如需有關設定服務安全性的詳細指示，請參閱 [分割合併安全性設定](sql-database-elastic-scale-split-merge-security-configuration.md)。</span><span class="sxs-lookup"><span data-stu-id="6a94b-140">For detailed instructions to configure the security of the service, refer to the [Split-Merge security configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

<span data-ttu-id="6a94b-141">為了執行簡單的測試部署以完成本教學課程，將會執行一組最基本的設定步驟，讓服務啟動並執行。</span><span class="sxs-lookup"><span data-stu-id="6a94b-141">For the purposes of a simple test deployment for this tutorial, a minimal set of configuration steps will be performed to get the service up and running.</span></span> <span data-ttu-id="6a94b-142">這些步驟只會啟用一個電腦/帳戶來與服務通訊。</span><span class="sxs-lookup"><span data-stu-id="6a94b-142">These steps enable only the one machine/account executing them to communicate with the service.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="6a94b-143">建立自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="6a94b-143">Create a self-signed certificate</span></span>
<span data-ttu-id="6a94b-144">使用 [Visual Studio 開發人員命令提示字元](http://msdn.microsoft.com/library/ms229859.aspx) 視窗建立新的目錄，並從這個目錄中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="6a94b-144">Create a new directory and from this directory execute the following command using a [Developer Command Prompt for Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) window:</span></span>

   ```
    makecert ^
    -n "CN=*.cloudapp.net" ^
    -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2" ^
    -a sha1 -len 2048 ^
    -sr currentuser -ss root ^
    -sv MyCert.pvk MyCert.cer
   ```

<span data-ttu-id="6a94b-145">將會要求您輸入密碼來保護私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="6a94b-145">You are asked for a password to protect the private key.</span></span> <span data-ttu-id="6a94b-146">輸入強式密碼並加以確認。</span><span class="sxs-lookup"><span data-stu-id="6a94b-146">Enter a strong password and confirm it.</span></span> <span data-ttu-id="6a94b-147">接著會提示您輸入之後要再次使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="6a94b-147">You are then prompted for the password to be used once more after that.</span></span> <span data-ttu-id="6a94b-148">最後，按一下 [是]  ，將它匯入受信任的憑證授權單位根目錄存放區。</span><span class="sxs-lookup"><span data-stu-id="6a94b-148">Click **Yes** at the end to import it to the Trusted Certification Authorities Root store.</span></span>

### <a name="create-a-pfx-file"></a><span data-ttu-id="6a94b-149">建立 PFX 檔案</span><span class="sxs-lookup"><span data-stu-id="6a94b-149">Create a PFX file</span></span>
<span data-ttu-id="6a94b-150">從執行 makecert 所在的相同視窗執行下列命令；使用您用來建立憑證的相同密碼：</span><span class="sxs-lookup"><span data-stu-id="6a94b-150">Execute the following command from the same window where makecert was executed; use the same password that you used to create the certificate:</span></span>

    pvk2pfx -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx -pi <password>

### <a name="import-the-client-certificate-into-the-personal-store"></a><span data-ttu-id="6a94b-151">將用戶端憑證匯入個人存放區</span><span class="sxs-lookup"><span data-stu-id="6a94b-151">Import the client certificate into the personal store</span></span>
1. <span data-ttu-id="6a94b-152">在 Windows 檔案總管中，按兩下 [MyCert.pfx] 。</span><span class="sxs-lookup"><span data-stu-id="6a94b-152">In Windows Explorer, double-click **MyCert.pfx**.</span></span>
2. <span data-ttu-id="6a94b-153">在 [憑證匯入精靈] 中，選取 [目前使用者]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="6a94b-153">In the **Certificate Import Wizard** select **Current User** and click **Next**.</span></span>
3. <span data-ttu-id="6a94b-154">確認檔案路徑，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="6a94b-154">Confirm the file path and click **Next**.</span></span>
4. <span data-ttu-id="6a94b-155">輸入密碼，保持核取 [包含所有延伸內容]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="6a94b-155">Type the password, leave **Include all extended properties** checked and click **Next**.</span></span>
5. <span data-ttu-id="6a94b-156">保持核取 [自動選取憑證存放區…]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="6a94b-156">Leave **Automatically select the certificate store[…]** checked and click **Next**.</span></span>
6. <span data-ttu-id="6a94b-157">按一下 [完成] 和 [確定]。</span><span class="sxs-lookup"><span data-stu-id="6a94b-157">Click **Finish** and **OK**.</span></span>

### <a name="upload-the-pfx-file-to-the-cloud-service"></a><span data-ttu-id="6a94b-158">將 PFX 檔案上傳至雲端服務</span><span class="sxs-lookup"><span data-stu-id="6a94b-158">Upload the PFX file to the cloud service</span></span>
1. <span data-ttu-id="6a94b-159">移至 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="6a94b-159">Go to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6a94b-160">選取 [雲端服務] 。</span><span class="sxs-lookup"><span data-stu-id="6a94b-160">Select **Cloud Services**.</span></span>
3. <span data-ttu-id="6a94b-161">選取您先前為分割/合併服務建立的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="6a94b-161">Select the cloud service you created above for the Split/Merge service.</span></span>
4. <span data-ttu-id="6a94b-162">按一下頂端功能表的 [憑證]  。</span><span class="sxs-lookup"><span data-stu-id="6a94b-162">Click **Certificates** on the top menu.</span></span>
5. <span data-ttu-id="6a94b-163">按一下底列的 [上傳]  。</span><span class="sxs-lookup"><span data-stu-id="6a94b-163">Click **Upload** in the bottom bar.</span></span>
6. <span data-ttu-id="6a94b-164">選取 PFX 檔案，並輸入與上述相同的密碼。</span><span class="sxs-lookup"><span data-stu-id="6a94b-164">Select the PFX file and enter the same password as above.</span></span>
7. <span data-ttu-id="6a94b-165">完成後，從清單中的新項目複製憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="6a94b-165">Once completed, copy the certificate thumbprint from the new entry in the list.</span></span>

### <a name="update-the-service-configuration-file"></a><span data-ttu-id="6a94b-166">更新服務組態檔</span><span class="sxs-lookup"><span data-stu-id="6a94b-166">Update the service configuration file</span></span>
<span data-ttu-id="6a94b-167">將上面複製的憑證指紋，貼到這些設定的憑證指紋/值屬性中。</span><span class="sxs-lookup"><span data-stu-id="6a94b-167">Paste the certificate thumbprint copied above into the thumbprint/value attribute of these settings.</span></span>
<span data-ttu-id="6a94b-168">背景工作角色：</span><span class="sxs-lookup"><span data-stu-id="6a94b-168">For the worker role:</span></span>
   ```
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="6a94b-169">Web 角色：</span><span class="sxs-lookup"><span data-stu-id="6a94b-169">For the web role:</span></span>

   ```
    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />
    <Setting name="AllowedClientCertificateThumbprints" value="" />
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="6a94b-170">請注意，在實際執行部署中，CA、加密、伺服器憑證和用戶端憑證應該使用個別憑證。</span><span class="sxs-lookup"><span data-stu-id="6a94b-170">Please note that for production deployments separate certificates should be used for the CA, for encryption, the Server certificate and client certificates.</span></span> <span data-ttu-id="6a94b-171">如需詳細指示，請參閱 [安全性設定](sql-database-elastic-scale-split-merge-security-configuration.md)。</span><span class="sxs-lookup"><span data-stu-id="6a94b-171">For detailed instructions on this, see [Security Configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

## <a name="deploy-your-service"></a><span data-ttu-id="6a94b-172">部署您的服務</span><span class="sxs-lookup"><span data-stu-id="6a94b-172">Deploy your service</span></span>
1. <span data-ttu-id="6a94b-173">移至 [Azure 入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="6a94b-173">Go to the [Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="6a94b-174">按一下左邊的 [雲端服務]  索引標籤，選取您稍早建立的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="6a94b-174">Click the **Cloud Services** tab on the left, and select the cloud service that you created earlier.</span></span>
3. <span data-ttu-id="6a94b-175">按一下 [儀表板] 。</span><span class="sxs-lookup"><span data-stu-id="6a94b-175">Click **Dashboard**.</span></span>
4. <span data-ttu-id="6a94b-176">選擇預備環境，然後按一下 [上傳新的預備部署] 。</span><span class="sxs-lookup"><span data-stu-id="6a94b-176">Choose the staging environment, then click **Upload a new staging deployment**.</span></span>
   
   ![預備][3]
5. <span data-ttu-id="6a94b-178">在對話方塊中，輸入部署的標籤。</span><span class="sxs-lookup"><span data-stu-id="6a94b-178">In the dialog box, enter a deployment label.</span></span> <span data-ttu-id="6a94b-179">在 [封裝] 和 [設定] 中，按一下 [從本機] 並選擇 **SplitMergeService.cspkg** 檔案和您稍早設定的 .cscfg 檔案。</span><span class="sxs-lookup"><span data-stu-id="6a94b-179">For both 'Package' and 'Configuration', click 'From Local' and choose the **SplitMergeService.cspkg** file and your .cscfg file that you configured earlier.</span></span>
6. <span data-ttu-id="6a94b-180">確定已核取 [即使一或多個角色包含單一執行個體也請部署]  核取方塊。</span><span class="sxs-lookup"><span data-stu-id="6a94b-180">Ensure that the checkbox labeled **Deploy even if one or more roles contain a single instance** is checked.</span></span>
7. <span data-ttu-id="6a94b-181">點按右下方的勾號按鈕，開始進行部署。</span><span class="sxs-lookup"><span data-stu-id="6a94b-181">Hit the tick button in the bottom right to begin the deployment.</span></span> <span data-ttu-id="6a94b-182">預期會需要幾分鐘才能完成。</span><span class="sxs-lookup"><span data-stu-id="6a94b-182">Expect it to take a few minutes to complete.</span></span>

   ![上傳][4]

## <a name="troubleshoot-the-deployment"></a><span data-ttu-id="6a94b-184">疑難排解部署</span><span class="sxs-lookup"><span data-stu-id="6a94b-184">Troubleshoot the deployment</span></span>
<span data-ttu-id="6a94b-185">如果 Web 角色無法上線，安全性設定可能有問題。</span><span class="sxs-lookup"><span data-stu-id="6a94b-185">If your web role fails to come online, it is likely a problem with the security configuration.</span></span> <span data-ttu-id="6a94b-186">請檢查 SSL 的設定如上所述。</span><span class="sxs-lookup"><span data-stu-id="6a94b-186">Check that the SSL is configured as described above.</span></span>

<span data-ttu-id="6a94b-187">如果背景工作角色無法上線，但 Web 角色成功上線，很可能是無法連接至您稍早建立的狀態資料庫。</span><span class="sxs-lookup"><span data-stu-id="6a94b-187">If your worker role fails to come online, but your web role succeeds, it is most likely a problem connecting to the status database that you created earlier.</span></span>

* <span data-ttu-id="6a94b-188">請確定您的 .cscfg 中的連接字串正確無誤。</span><span class="sxs-lookup"><span data-stu-id="6a94b-188">Make sure that the connection string in your .cscfg is accurate.</span></span>
* <span data-ttu-id="6a94b-189">請檢查伺服器和資料庫均存在，而且使用者識別碼與密碼皆正確無誤。</span><span class="sxs-lookup"><span data-stu-id="6a94b-189">Check that the server and database exist, and that the user id and password are correct.</span></span>
* <span data-ttu-id="6a94b-190">在 Azure SQL DB 中，連接字串的格式應該為：</span><span class="sxs-lookup"><span data-stu-id="6a94b-190">For Azure SQL DB, the connection string should be of the form:</span></span>

   ```  
   Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
   ```

* <span data-ttu-id="6a94b-191">確定伺服器名稱不是以 **https://** 開頭。</span><span class="sxs-lookup"><span data-stu-id="6a94b-191">Ensure that the server name does not begin with **https://**.</span></span>
* <span data-ttu-id="6a94b-192">請確定您的 Azure SQL DB 伺服器允許 Azure 服務進行連接。</span><span class="sxs-lookup"><span data-stu-id="6a94b-192">Ensure that your Azure SQL DB server allows Azure Services to connect to it.</span></span> <span data-ttu-id="6a94b-193">若要這樣做，請開啟 https://manage.windowsazure.com，按一下左邊的 [SQL Database]，按一下頂端的 [伺服器]，然後選取您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="6a94b-193">To do this, open https://manage.windowsazure.com, click “SQL Databases” on the left, click “Servers” at the top, and select your server.</span></span> <span data-ttu-id="6a94b-194">按一下頂端的 [設定]，並確定 [Azure 服務] 設定已設為 [是]。</span><span class="sxs-lookup"><span data-stu-id="6a94b-194">Click **Configure** at the top and ensure that the **Azure Services** setting is set to “Yes”.</span></span> <span data-ttu-id="6a94b-195">(請參閱本文開頭的＜必要條件＞一節)。</span><span class="sxs-lookup"><span data-stu-id="6a94b-195">(See the Prerequisites section at the top of this article).</span></span>

## <a name="test-the-service-deployment"></a><span data-ttu-id="6a94b-196">測試服務部署</span><span class="sxs-lookup"><span data-stu-id="6a94b-196">Test the service deployment</span></span>
### <a name="connect-with-a-web-browser"></a><span data-ttu-id="6a94b-197">使用網頁瀏覽器連接</span><span class="sxs-lookup"><span data-stu-id="6a94b-197">Connect with a web browser</span></span>
<span data-ttu-id="6a94b-198">決定分割合併服務的 Web 端點。</span><span class="sxs-lookup"><span data-stu-id="6a94b-198">Determine the web endpoint of your Split-Merge service.</span></span> <span data-ttu-id="6a94b-199">您可以在 Azure 傳統入口網站中找到此端點，請移至雲端服務的 [儀表板]，查看右邊的 [網站 URL]。</span><span class="sxs-lookup"><span data-stu-id="6a94b-199">You can find this in the Azure Classic Portal by going to the **Dashboard** of your cloud service and looking under **Site URL** on the right side.</span></span> <span data-ttu-id="6a94b-200">由於預設安全性設定會停用 HTTP 端點，因此以 **https://** 取代 **http://**。</span><span class="sxs-lookup"><span data-stu-id="6a94b-200">Replace **http://** with **https://** since the default security settings disable the HTTP endpoint.</span></span> <span data-ttu-id="6a94b-201">在瀏覽器中載入此 URL 的網頁。</span><span class="sxs-lookup"><span data-stu-id="6a94b-201">Load the page for this URL into your browser.</span></span>

### <a name="test-with-powershell-scripts"></a><span data-ttu-id="6a94b-202">使用 PowerShell 指令碼進行測試</span><span class="sxs-lookup"><span data-stu-id="6a94b-202">Test with PowerShell scripts</span></span>
<span data-ttu-id="6a94b-203">執行內含的範例 PowerShell 指令碼即可測試部署和您的環境。</span><span class="sxs-lookup"><span data-stu-id="6a94b-203">The deployment and your environment can be tested by running the included sample PowerShell scripts.</span></span>

<span data-ttu-id="6a94b-204">內含的指令碼檔案：</span><span class="sxs-lookup"><span data-stu-id="6a94b-204">The script files included are:</span></span>

1. <span data-ttu-id="6a94b-205">**SetupSampleSplitMergeEnvironment.ps1** - 設定分割/合併的測試資料層 (請參閱下表中的詳細說明)</span><span class="sxs-lookup"><span data-stu-id="6a94b-205">**SetupSampleSplitMergeEnvironment.ps1** - sets up a test data tier for Split/Merge (see table below for detailed description)</span></span>
2. <span data-ttu-id="6a94b-206">**ExecuteSampleSplitMerge.ps1** - 在測試資料層執行測試作業 (請參閱下表中的詳細說明)</span><span class="sxs-lookup"><span data-stu-id="6a94b-206">**ExecuteSampleSplitMerge.ps1** - executes test operations on the test data tier (see table below for detailed description)</span></span>
3. <span data-ttu-id="6a94b-207">**GetMappings.ps1** - 可印出目前分區對應狀態的最上層範例指令碼。</span><span class="sxs-lookup"><span data-stu-id="6a94b-207">**GetMappings.ps1** - top-level sample script that prints out the current state of the shard mappings.</span></span>
4. <span data-ttu-id="6a94b-208">**ShardManagement.psm1** - 包裝 ShardManagement API 的協助程式指令碼</span><span class="sxs-lookup"><span data-stu-id="6a94b-208">**ShardManagement.psm1**  - helper script that wraps the ShardManagement API</span></span>
5. <span data-ttu-id="6a94b-209">**SqlDatabaseHelpers.psm1** - 用來建立及管理 SQL 資料庫的協助程式指令碼</span><span class="sxs-lookup"><span data-stu-id="6a94b-209">**SqlDatabaseHelpers.psm1** - helper script for creating and managing SQL databases</span></span>
   
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="6a94b-210">PowerShell 檔案</span><span class="sxs-lookup"><span data-stu-id="6a94b-210">PowerShell file</span></span></th>
       <th><span data-ttu-id="6a94b-211">步驟</span><span class="sxs-lookup"><span data-stu-id="6a94b-211">Steps</span></span></th>
     </tr>
     <tr>
       <th rowspan="5"><span data-ttu-id="6a94b-212">SetupSampleSplitMergeEnvironment.ps1</span><span class="sxs-lookup"><span data-stu-id="6a94b-212">SetupSampleSplitMergeEnvironment.ps1</span></span></th>
       <td>1.    <span data-ttu-id="6a94b-213">建立分區對應管理員資料庫</span><span class="sxs-lookup"><span data-stu-id="6a94b-213">Creates a shard map manager database</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="6a94b-214">建立 2 個分區資料庫。</span><span class="sxs-lookup"><span data-stu-id="6a94b-214">Creates 2 shard databases.</span></span>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="6a94b-215">建立這些資料庫的分區對應 (刪除這些資料庫上的任何現有分區對應)。</span><span class="sxs-lookup"><span data-stu-id="6a94b-215">Creates a shard map for those database (deletes any existing shard maps on those databases).</span></span> </td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="6a94b-216">在這兩個分區中建立小型範例資料表，並填入其中一個分區中的資料表。</span><span class="sxs-lookup"><span data-stu-id="6a94b-216">Creates a small sample table in both the shards, and populates the table in one of the shards.</span></span></td>
     </tr>
     <tr>
       <td>5.    <span data-ttu-id="6a94b-217">宣告分區化資料表的 SchemaInfo。</span><span class="sxs-lookup"><span data-stu-id="6a94b-217">Declares the SchemaInfo for the sharded table.</span></span></td>
     </tr>
   </table>
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="6a94b-218">PowerShell 檔案</span><span class="sxs-lookup"><span data-stu-id="6a94b-218">PowerShell file</span></span></th>
       <th><span data-ttu-id="6a94b-219">步驟</span><span class="sxs-lookup"><span data-stu-id="6a94b-219">Steps</span></span></th>
     </tr>
   <tr>
       <th rowspan="4"><span data-ttu-id="6a94b-220">ExecuteSampleSplitMerge.ps1</span><span class="sxs-lookup"><span data-stu-id="6a94b-220">ExecuteSampleSplitMerge.ps1</span></span> </th>
       <td>1.    <span data-ttu-id="6a94b-221">將分割要求傳送至分割合併服務 Web 前端，要求將第一個分區的資料分割一半給第二個分區。</span><span class="sxs-lookup"><span data-stu-id="6a94b-221">Sends a split request to the Split-Merge Service web frontend, which splits half the data from the first shard to the second shard.</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="6a94b-222">向 Web 前端輪詢分割要求的狀態，並等待完成要求。</span><span class="sxs-lookup"><span data-stu-id="6a94b-222">Polls the web frontend for the split request status and waits until the request completes.</span></span></td>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="6a94b-223">將合併要求傳送至分割合併服務 Web 前端，要求將第二個分區的資料移回到第一個分區。</span><span class="sxs-lookup"><span data-stu-id="6a94b-223">Sends a merge request to the Split-Merge Service web frontend, which moves the data from the second shard back to the first shard.</span></span></td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="6a94b-224">向 Web 前端輪詢合併要求的狀態，並等待完成要求。</span><span class="sxs-lookup"><span data-stu-id="6a94b-224">Polls the web frontend for the merge request status and waits until the request completes.</span></span></td>
     </tr>
   </table>
   
## <a name="use-powershell-to-verify-your-deployment"></a><span data-ttu-id="6a94b-225">使用 PowerShell 來驗證您的部署</span><span class="sxs-lookup"><span data-stu-id="6a94b-225">Use PowerShell to verify your deployment</span></span>
1. <span data-ttu-id="6a94b-226">開啟新的 PowerShell 視窗，並瀏覽至您下載分割-合併套件的目錄，然後瀏覽到 "powershell" 目錄。</span><span class="sxs-lookup"><span data-stu-id="6a94b-226">Open a new PowerShell window and navigate to the directory where you downloaded the Split-Merge package, and then navigate into the “powershell” directory.</span></span>
2. <span data-ttu-id="6a94b-227">建立 Azure SQL Database 伺服器 (或選擇現有的伺服器)，其中將會建立分區對應管理員和分區。</span><span class="sxs-lookup"><span data-stu-id="6a94b-227">Create an Azure SQL database server (or choose an existing server) where the shard map manager and shards will be created.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6a94b-228">SetupSampleSplitMergeEnvironment.ps1 指令碼預設會在相同的伺服器上建立所有資料庫，以簡化指令碼。</span><span class="sxs-lookup"><span data-stu-id="6a94b-228">The SetupSampleSplitMergeEnvironment.ps1 script creates all these databases on the same server by default to keep the script simple.</span></span> <span data-ttu-id="6a94b-229">這不是分割合併服務本身的限制。</span><span class="sxs-lookup"><span data-stu-id="6a94b-229">This is not a restriction of the Split-Merge Service itself.</span></span>
   >
   
   <span data-ttu-id="6a94b-230">需要有具備 DB 讀取/寫入存取權的 SQL 驗證登入，分割合併服務才能移動資料和更新分區對應。</span><span class="sxs-lookup"><span data-stu-id="6a94b-230">A SQL authentication login with read/write access to the DBs will be needed for the Split-Merge service to move data and update the shard map.</span></span> <span data-ttu-id="6a94b-231">因為分割合併服務是在雲端執行，目前不支援整合式驗證。</span><span class="sxs-lookup"><span data-stu-id="6a94b-231">Since the Split-Merge Service runs in the cloud, it does not currently support Integrated Authentication.</span></span>
   
   <span data-ttu-id="6a94b-232">請確定 Azure SQL server 設定為允許從執行這些指令碼的電腦 IP 位址存取。</span><span class="sxs-lookup"><span data-stu-id="6a94b-232">Make sure the Azure SQL server is configured to allow access from the IP address of the machine running these scripts.</span></span> <span data-ttu-id="6a94b-233">您可以在 [Azure SQL server / 設定 / 允許的 IP 位址] 下找到這項設定。</span><span class="sxs-lookup"><span data-stu-id="6a94b-233">You can find this setting under the Azure SQL server / configuration / allowed IP addresses.</span></span>
3. <span data-ttu-id="6a94b-234">執行 SetupSampleSplitMergeEnvironment.ps1 指令碼以建立範例環境。</span><span class="sxs-lookup"><span data-stu-id="6a94b-234">Execute the SetupSampleSplitMergeEnvironment.ps1 script to create the sample environment.</span></span>
   
   <span data-ttu-id="6a94b-235">執行這個指令碼將會從分區對應管理員資料庫和分區上，清除任何現有的分區對應管理資料結構。</span><span class="sxs-lookup"><span data-stu-id="6a94b-235">Running this script will wipe out any existing shard map management data structures on the shard map manager database and the shards.</span></span> <span data-ttu-id="6a94b-236">如果您想要重新初始化分區對應或分區，最好重新執行此指令碼。</span><span class="sxs-lookup"><span data-stu-id="6a94b-236">It may be useful to rerun the script if you wish to re-initialize the shard map or shards.</span></span>
   
   <span data-ttu-id="6a94b-237">範例命令列：</span><span class="sxs-lookup"><span data-stu-id="6a94b-237">Sample command line:</span></span>

   ```   
     .\SetupSampleSplitMergeEnvironment.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'
   ```      
4. <span data-ttu-id="6a94b-238">執行 Getmappings.ps1 指令碼以檢視範例環境中目前存在的對應。</span><span class="sxs-lookup"><span data-stu-id="6a94b-238">Execute the Getmappings.ps1 script to view the mappings that currently exist in the sample environment.</span></span>
   
   ```
     .\GetMappings.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'

   ```         
5. <span data-ttu-id="6a94b-239">執行 ExecuteSampleSplitMerge.ps1 指令碼，以執行分割作業 (將第一個分區的一半資料移至第二個分區)，然後執行合併作業 (將資料移回至第一個分區)。</span><span class="sxs-lookup"><span data-stu-id="6a94b-239">Execute the ExecuteSampleSplitMerge.ps1 script to execute a split operation (moving half the data on the first shard to the second shard) and then a merge operation (moving the data back onto the first shard).</span></span> <span data-ttu-id="6a94b-240">如果您設定 SSL，而且保持停用 http 端點，請確定您改為使用 https:// 端點。</span><span class="sxs-lookup"><span data-stu-id="6a94b-240">If you configured SSL and left the http endpoint disabled, ensure that you use the https:// endpoint instead.</span></span>
   
   <span data-ttu-id="6a94b-241">範例命令列：</span><span class="sxs-lookup"><span data-stu-id="6a94b-241">Sample command line:</span></span>

   ```   
     .\ExecuteSampleSplitMerge.ps1
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net' 
         -SplitMergeServiceEndpoint 'https://mysplitmergeservice.cloudapp.net' 
         -CertificateThumbprint '0123456789abcdef0123456789abcdef01234567'
   ```      
   
   <span data-ttu-id="6a94b-242">如果您收到下列錯誤，很可能是 Web 端點的憑證有問題。</span><span class="sxs-lookup"><span data-stu-id="6a94b-242">If you receive the below error, it is most likely a problem with your Web endpoint’s certificate.</span></span> <span data-ttu-id="6a94b-243">使用您最愛的網頁瀏覽器嘗試連線到的 Web 端點，並檢查是否有憑證錯誤。</span><span class="sxs-lookup"><span data-stu-id="6a94b-243">Try connecting to the Web endpoint with your favorite Web browser and check if there is a certificate error.</span></span>
   
     ```
     Invoke-WebRequest : The underlying connection was closed: Could not establish trust relationship for the SSL/TLSsecure channel.
     ```
   
   <span data-ttu-id="6a94b-244">如果成功，輸出應該看起來如下：</span><span class="sxs-lookup"><span data-stu-id="6a94b-244">If it succeeded, the output should look like the below:</span></span>
   
   ```
   > .\ExecuteSampleSplitMerge.ps1 -UserName 'mysqluser' -Password 'MySqlPassw0rd' -ShardMapManagerServerName 'abcdefghij.database.windows.net' -SplitMergeServiceEndpoint 'http://mysplitmergeservice.cloudapp.net' -CertificateThumbprint 0123456789abcdef0123456789abcdef01234567
   > Sending split request
   > Began split operation with id dc68dfa0-e22b-4823-886a-9bdc903c80f3
   > Polling split-merge request status. Press Ctrl-C to end
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source to target shard.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Waiting for reference tables copy     completion.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source to target shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing the request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > Sending merge request
   > Began merge operation with id 6ffc308f-d006-466b-b24e-857242ec5f66
   > Polling request status. Press Ctrl-C to end
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source to target shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing the request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > 
   ```
6. <span data-ttu-id="6a94b-245">試驗其他資料類型！</span><span class="sxs-lookup"><span data-stu-id="6a94b-245">Experiment with other data types!</span></span> <span data-ttu-id="6a94b-246">所有這些指令碼都採用可供指定金鑰類型的選擇性 -ShardKeyType 參數。</span><span class="sxs-lookup"><span data-stu-id="6a94b-246">All of these scripts take an optional -ShardKeyType parameter that allows you to specify the key type.</span></span> <span data-ttu-id="6a94b-247">預設值為 Int32，但您也可以指定 Int64、Guid 或二進位。</span><span class="sxs-lookup"><span data-stu-id="6a94b-247">The default is Int32, but you can also specify Int64, Guid, or Binary.</span></span>

## <a name="create-requests"></a><span data-ttu-id="6a94b-248">建立要求</span><span class="sxs-lookup"><span data-stu-id="6a94b-248">Create requests</span></span>
<span data-ttu-id="6a94b-249">您可以透過 Web UI，或匯入並使用將透過 Web 角色提交需求的 SplitMerge.psm1 PowerShell 模組，以使用此服務。</span><span class="sxs-lookup"><span data-stu-id="6a94b-249">The service can be used either by using the web UI or by importing and using the SplitMerge.psm1 PowerShell module which will submit your requests through the web role.</span></span>

<span data-ttu-id="6a94b-250">此服務可以移動分區化資料表和參考資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="6a94b-250">The service can move data in both sharded tables and reference tables.</span></span> <span data-ttu-id="6a94b-251">分區資料表具有分區化索引鍵資料行，且在每個分區上有不同的資料列資料。</span><span class="sxs-lookup"><span data-stu-id="6a94b-251">A sharded table has a sharding key column and has different row data on each shard.</span></span> <span data-ttu-id="6a94b-252">參考資料表並未分區，所以每個分區包含相同的資料列資料。</span><span class="sxs-lookup"><span data-stu-id="6a94b-252">A reference table is not sharded so it contains the same row data on every shard.</span></span> <span data-ttu-id="6a94b-253">參考資料表適用於不常變更的資料，且在查詢中用來「聯結」分區化資料表。</span><span class="sxs-lookup"><span data-stu-id="6a94b-253">Reference tables are useful for data that does not change often and is used to JOIN with sharded tables in queries.</span></span>

<span data-ttu-id="6a94b-254">若要執行分割合併作業，您必須宣告想要移動的分區化資料表和參考資料表。</span><span class="sxs-lookup"><span data-stu-id="6a94b-254">In order to perform a split-merge operation, you must declare the sharded tables and reference tables that you want to have moved.</span></span> <span data-ttu-id="6a94b-255">這是透過 **SchemaInfo** API 來達成。</span><span class="sxs-lookup"><span data-stu-id="6a94b-255">This is accomplished with the **SchemaInfo** API.</span></span> <span data-ttu-id="6a94b-256">此 API 位於 **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** 命名空間中。</span><span class="sxs-lookup"><span data-stu-id="6a94b-256">This API is in the **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** namespace.</span></span>

1. <span data-ttu-id="6a94b-257">對於每個分區資料表，建立 **ShardedTableInfo** 物件，以描述資料表的父結構描述名稱 (選擇性，預設值為 "dbo")、資料表名稱，以及該資料表中包含分區化索引鍵的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="6a94b-257">For each sharded table, create a **ShardedTableInfo** object describing the table’s parent schema name (optional, defaults to “dbo”), the table name, and the column name in that table that contains the sharding key.</span></span>
2. <span data-ttu-id="6a94b-258">對於每個參考資料表，建立 **ReferenceTableInfo** 物件，以描述資料表的父結構描述名稱 (選擇性，預設為 "dbo") 和資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="6a94b-258">For each reference table, create a **ReferenceTableInfo** object describing the table’s parent schema name (optional, defaults to “dbo”) and the table name.</span></span>
3. <span data-ttu-id="6a94b-259">將上述 TableInfo 物件新增至新的 **SchemaInfo** 物件。</span><span class="sxs-lookup"><span data-stu-id="6a94b-259">Add the above TableInfo objects to a new **SchemaInfo** object.</span></span>
4. <span data-ttu-id="6a94b-260">取得 **ShardMapManager** 物件的參考，並呼叫 **GetSchemaInfoCollection**。</span><span class="sxs-lookup"><span data-stu-id="6a94b-260">Get a reference to a **ShardMapManager** object, and call **GetSchemaInfoCollection**.</span></span>
5. <span data-ttu-id="6a94b-261">將 **SchemaInfo** 新增至 **SchemaInfoCollection**，並提供分區對應名稱。</span><span class="sxs-lookup"><span data-stu-id="6a94b-261">Add the **SchemaInfo** to the **SchemaInfoCollection**, providing the shard map name.</span></span>

<span data-ttu-id="6a94b-262">在 SetupSampleSplitMergeEnvironment.ps1 指令碼中可以看見這個範例。</span><span class="sxs-lookup"><span data-stu-id="6a94b-262">An example of this can be seen in the SetupSampleSplitMergeEnvironment.ps1 script.</span></span>

<span data-ttu-id="6a94b-263">「分割-合併」服務不會為您建立目標資料庫 (或資料庫中任何資料表的結構描述)。</span><span class="sxs-lookup"><span data-stu-id="6a94b-263">The Split-Merge service does not create the target database (or schema for any tables in the database) for you.</span></span> <span data-ttu-id="6a94b-264">將要求傳送至服務之前，必須先建立它們。</span><span class="sxs-lookup"><span data-stu-id="6a94b-264">They must be pre-created before sending a request to the service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="6a94b-265">疑難排解</span><span class="sxs-lookup"><span data-stu-id="6a94b-265">Troubleshooting</span></span>
<span data-ttu-id="6a94b-266">執行範例 powershell 指令碼時，您可能會看到以下訊息：</span><span class="sxs-lookup"><span data-stu-id="6a94b-266">You may see the below message when running the sample powershell scripts:</span></span>

   ```
   Invoke-WebRequest : The underlying connection was closed: Could not establish trust relationship for the SSL/TLS secure channel.
   ```

<span data-ttu-id="6a94b-267">此錯誤表示您的 SSL 憑證未正確設定。</span><span class="sxs-lookup"><span data-stu-id="6a94b-267">This error means that your SSL certificate is not configured correctly.</span></span> <span data-ttu-id="6a94b-268">請遵循＜使用網頁瀏覽器連接＞一節的指示。</span><span class="sxs-lookup"><span data-stu-id="6a94b-268">Please follow the instructions in section 'Connecting with a web browser'.</span></span>

<span data-ttu-id="6a94b-269">若無法提交要求，您可能會看到：</span><span class="sxs-lookup"><span data-stu-id="6a94b-269">If you cannot submit requests you may see this:</span></span>

```
[Exception] System.Data.SqlClient.SqlException (0x80131904): Could not find stored procedure 'dbo.InsertRequest'. 
```

<span data-ttu-id="6a94b-270">在此情況下，請檢查組態檔，特別是 **WorkerRoleSynchronizationStorageAccountConnectionString**的設定。</span><span class="sxs-lookup"><span data-stu-id="6a94b-270">In this case, check your configuration file, in particular the setting for **WorkerRoleSynchronizationStorageAccountConnectionString**.</span></span> <span data-ttu-id="6a94b-271">這個錯誤通常表示背景工作角色無法在第一次使用時成功初始化中繼資料資料庫。</span><span class="sxs-lookup"><span data-stu-id="6a94b-271">This error typically indicates that the worker role could not successfully initialize the metadata database on first use.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/allowed-services.png
[2]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/manage.png
[3]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/staging.png
[4]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/upload.png
[5]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/storage.png

