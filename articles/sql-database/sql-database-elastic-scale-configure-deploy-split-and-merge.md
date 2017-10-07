---
title: "aaaDeploy 分割合併服務 |Microsoft 文件"
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
ms.openlocfilehash: 6fef641cbc1e73ce34a851c53298a072dade8f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-split-merge-service"></a><span data-ttu-id="b2c7d-103">部署分割合併服務</span><span class="sxs-lookup"><span data-stu-id="b2c7d-103">Deploy a split-merge service</span></span>
<span data-ttu-id="b2c7d-104">hello 分割合併工具可讓您在分區化資料庫之間移動資料。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-104">hello split-merge tool lets you move data between sharded databases.</span></span> <span data-ttu-id="b2c7d-105">請參閱 [在相應放大的雲端資料庫之間移動資料](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="b2c7d-105">See [Moving data between scaled-out cloud databases](sql-database-elastic-scale-overview-split-and-merge.md)</span></span>

## <a name="download-hello-split-merge-packages"></a><span data-ttu-id="b2c7d-106">下載 hello 分割合併封裝</span><span class="sxs-lookup"><span data-stu-id="b2c7d-106">Download hello Split-Merge packages</span></span>
1. <span data-ttu-id="b2c7d-107">下載 hello 最新的 NuGet 版本從[NuGet](http://docs.nuget.org/docs/start-here/installing-nuget)。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-107">Download hello latest NuGet version from [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span></span>
2. <span data-ttu-id="b2c7d-108">開啟命令提示字元並瀏覽 toohello nuget.exe 的下載位置的目錄。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-108">Open a command prompt and navigate toohello directory where you downloaded nuget.exe.</span></span> <span data-ttu-id="b2c7d-109">hello 下載包含 PowerShell commmands。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-109">hello download includes PowerShell commmands.</span></span>
3. <span data-ttu-id="b2c7d-110">下載 hello 最新的分割合併封裝到 hello 目前目錄中以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="b2c7d-110">Download hello latest Split-Merge package into hello current directory with hello below command:</span></span>
   ```
   nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge
   ```  

<span data-ttu-id="b2c7d-111">hello 檔案會放置於名為**Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x**其中*x.x.xxx.x*反映 hello 版本號碼。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-111">hello files are placed in a directory named **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** where *x.x.xxx.x* reflects hello version number.</span></span> <span data-ttu-id="b2c7d-112">尋找 hello 的分割合併服務檔案 hello **content\splitmerge\service**子目錄，hello 分割合併 PowerShell 指令碼 （和必要的用戶端.dll 檔） 中 hello **content\splitmerge\powershell**子目錄。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-112">Find hello split-merge Service files in hello **content\splitmerge\service** sub-directory, and hello Split-Merge PowerShell scripts (and required client .dlls) in hello **content\splitmerge\powershell** sub-directory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2c7d-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="b2c7d-113">Prerequisites</span></span>
1. <span data-ttu-id="b2c7d-114">建立 Azure SQL DB 資料庫，將用作 hello 分割合併狀態資料庫。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-114">Create an Azure SQL DB database that will be used as hello split-merge status database.</span></span> <span data-ttu-id="b2c7d-115">移 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-115">Go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b2c7d-116">建立新的 **SQL Database**。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-116">Create a new **SQL Database**.</span></span> <span data-ttu-id="b2c7d-117">提供 hello 資料庫的名稱，並建立新的系統管理員和密碼。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-117">Give hello database a name and create a new administrator and password.</span></span> <span data-ttu-id="b2c7d-118">是確定 toorecord hello 名稱和密碼，供日後使用。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-118">Be sure toorecord hello name and password for later use.</span></span>
2. <span data-ttu-id="b2c7d-119">請確定您的 Azure SQL DB 伺服器允許 Azure 服務 tooconnect tooit。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-119">Ensure that your Azure SQL DB server allows Azure Services tooconnect tooit.</span></span> <span data-ttu-id="b2c7d-120">在 hello 入口網站中 hello**防火牆設定**，確保該 hello **tooAzure 服務允許存取**設定為太**上**。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-120">In hello portal, in hello **Firewall Settings**, ensure that hello **Allow access tooAzure Services** setting is set too**On**.</span></span> <span data-ttu-id="b2c7d-121">按一下 [儲存] 圖示的 hello。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-121">Click hello "save" icon.</span></span>
   
   ![允許的服務][1]
3. <span data-ttu-id="b2c7d-123">建立要用於診斷輸出的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-123">Create an Azure Storage account that will be used for diagnostics output.</span></span> <span data-ttu-id="b2c7d-124">移 toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-124">Go toohello Azure Portal.</span></span> <span data-ttu-id="b2c7d-125">Hello 左列中，按一下**新增**，按一下 **資料 + 儲存體**，然後**儲存體**。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-125">In hello left bar, click **New**, click **Data + Storage**, then **Storage**.</span></span>
4. <span data-ttu-id="b2c7d-126">建立將包含分割合併服務的 Azure 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-126">Create an Azure Cloud Service that will contain your Split-Merge service.</span></span>  <span data-ttu-id="b2c7d-127">移 toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-127">Go toohello Azure Portal.</span></span> <span data-ttu-id="b2c7d-128">Hello 左列中，按一下**新增**，然後**計算**，**雲端服務**，和**建立**。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-128">In hello left bar, click **New**, then **Compute**, **Cloud Service**, and **Create**.</span></span> 

## <a name="configure-your-split-merge-service"></a><span data-ttu-id="b2c7d-129">設定分割合併服務</span><span class="sxs-lookup"><span data-stu-id="b2c7d-129">Configure your Split-Merge service</span></span>
### <a name="split-merge-service-configuration"></a><span data-ttu-id="b2c7d-130">分割合併服務組態</span><span class="sxs-lookup"><span data-stu-id="b2c7d-130">Split-Merge service configuration</span></span>
1. <span data-ttu-id="b2c7d-131">在您下載 hello 分割合併組件的 hello 資料夾中建立 的副本 hello **ServiceConfiguration.Template.cscfg**檔案一起出貨**SplitMergeService.cspkg**並將它重新命名**ServiceConfiguration.cscfg**。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-131">In hello folder where you downloaded hello Split-Merge assemblies, create a copy of hello **ServiceConfiguration.Template.cscfg** file that shipped alongside **SplitMergeService.cspkg** and rename it **ServiceConfiguration.cscfg**.</span></span>
2. <span data-ttu-id="b2c7d-132">開啟**ServiceConfiguration.cscfg**驗證的輸入，例如 hello 格式的憑證指紋的 Visual Studio 這類文字編輯器中。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-132">Open **ServiceConfiguration.cscfg** in a text editor such as Visual Studio that validates inputs such as hello format of certificate thumbprints.</span></span>
3. <span data-ttu-id="b2c7d-133">建立新的資料庫或選擇現有的資料庫 tooserve 做為分割合併作業的 hello 狀態資料庫並擷取 hello 該資料庫的連接字串。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-133">Create a new database or choose an existing database tooserve as hello status database for Split-Merge operations and retrieve hello connection string of that database.</span></span> 
   
   > [!IMPORTANT]
   > <span data-ttu-id="b2c7d-134">此時，hello 狀態資料庫必須使用 hello 拉丁文定序 (SQL\_Latin1\_一般\_CP1\_CI\_AS)。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-134">At this time, hello status database must use hello Latin  collation (SQL\_Latin1\_General\_CP1\_CI\_AS).</span></span> <span data-ttu-id="b2c7d-135">如需詳細資訊，請參閱 [Windows 定序名稱 (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-135">For more information, see [Windows Collation Name (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span></span>
   >

   <span data-ttu-id="b2c7d-136">使用 Azure SQL DB、 hello 連接字串通常是 hello 表單的：</span><span class="sxs-lookup"><span data-stu-id="b2c7d-136">With Azure SQL DB, hello connection string typically is of hello form:</span></span>
      ```
      Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
      ```

4. <span data-ttu-id="b2c7d-137">輸入此連接字串 hello cscfg 檔案中這兩個 hello **SplitMergeWeb**和**SplitMergeWorker** hello ElasticScaleMetadata 設定中的角色區段。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-137">Enter this connection string in hello cscfg file in both hello **SplitMergeWeb** and **SplitMergeWorker** role sections in hello ElasticScaleMetadata setting.</span></span>
5. <span data-ttu-id="b2c7d-138">Hello **SplitMergeWorker**角色中，輸入有效的連接字串 tooAzure 儲存體 hello **WorkerRoleSynchronizationStorageAccountConnectionString**設定。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-138">For hello **SplitMergeWorker** role, enter a valid connection string tooAzure storage for hello **WorkerRoleSynchronizationStorageAccountConnectionString** setting.</span></span>

### <a name="configure-security"></a><span data-ttu-id="b2c7d-139">設定安全性</span><span class="sxs-lookup"><span data-stu-id="b2c7d-139">Configure security</span></span>
<span data-ttu-id="b2c7d-140">Hello 服務的 tooconfigure hello 安全性的詳細的指示，請參閱 toohello[分割合併安全性組態](sql-database-elastic-scale-split-merge-security-configuration.md)。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-140">For detailed instructions tooconfigure hello security of hello service, refer toohello [Split-Merge security configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

<span data-ttu-id="b2c7d-141">本教學課程的簡單的測試部署的 hello 用途，最基本的組態步驟將會執行 tooget hello 服務啟動並執行。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-141">For hello purposes of a simple test deployment for this tutorial, a minimal set of configuration steps will be performed tooget hello service up and running.</span></span> <span data-ttu-id="b2c7d-142">這些步驟會啟用只 hello 一個機器/帳戶執行它們 toocommunicate 與 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-142">These steps enable only hello one machine/account executing them toocommunicate with hello service.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="b2c7d-143">建立自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="b2c7d-143">Create a self-signed certificate</span></span>
<span data-ttu-id="b2c7d-144">建立新的目錄，下列命令會使用這個目錄執行 hello 從[Visual Studio 的開發人員命令提示字元](http://msdn.microsoft.com/library/ms229859.aspx)視窗：</span><span class="sxs-lookup"><span data-stu-id="b2c7d-144">Create a new directory and from this directory execute hello following command using a [Developer Command Prompt for Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) window:</span></span>

   ```
    makecert ^
    -n "CN=*.cloudapp.net" ^
    -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2" ^
    -a sha1 -len 2048 ^
    -sr currentuser -ss root ^
    -sv MyCert.pvk MyCert.cer
   ```

<span data-ttu-id="b2c7d-145">會要求您輸入的密碼 tooprotect hello 私用金鑰。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-145">You are asked for a password tooprotect hello private key.</span></span> <span data-ttu-id="b2c7d-146">輸入強式密碼並加以確認。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-146">Enter a strong password and confirm it.</span></span> <span data-ttu-id="b2c7d-147">您接著會提示輸入 hello 密碼 toobe 之後，一次使用。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-147">You are then prompted for hello password toobe used once more after that.</span></span> <span data-ttu-id="b2c7d-148">按一下**是**在 hello 結束 tooimport 它 toohello 受信任憑證授權單位的根存放區。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-148">Click **Yes** at hello end tooimport it toohello Trusted Certification Authorities Root store.</span></span>

### <a name="create-a-pfx-file"></a><span data-ttu-id="b2c7d-149">建立 PFX 檔案</span><span class="sxs-lookup"><span data-stu-id="b2c7d-149">Create a PFX file</span></span>
<span data-ttu-id="b2c7d-150">執行下列命令從 hello hello 執行 makecert 所在; 相同的視窗使用 hello 相同的密碼，您使用的 toocreate hello 憑證：</span><span class="sxs-lookup"><span data-stu-id="b2c7d-150">Execute hello following command from hello same window where makecert was executed; use hello same password that you used toocreate hello certificate:</span></span>

    pvk2pfx -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx -pi <password>

### <a name="import-hello-client-certificate-into-hello-personal-store"></a><span data-ttu-id="b2c7d-151">Hello 用戶端憑證匯入到個人存放區 hello</span><span class="sxs-lookup"><span data-stu-id="b2c7d-151">Import hello client certificate into hello personal store</span></span>
1. <span data-ttu-id="b2c7d-152">在 Windows 檔案總管中，按兩下 [MyCert.pfx] 。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-152">In Windows Explorer, double-click **MyCert.pfx**.</span></span>
2. <span data-ttu-id="b2c7d-153">在 [hello**憑證匯入精靈**選取**目前使用者**按一下**下一步]**。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-153">In hello **Certificate Import Wizard** select **Current User** and click **Next**.</span></span>
3. <span data-ttu-id="b2c7d-154">確認 hello 檔案路徑，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-154">Confirm hello file path and click **Next**.</span></span>
4. <span data-ttu-id="b2c7d-155">輸入 hello 密碼保持**包含所有延伸的屬性**檢查，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-155">Type hello password, leave **Include all extended properties** checked and click **Next**.</span></span>
5. <span data-ttu-id="b2c7d-156">保留**hello 自動選取憑證存放區 […]**檢查，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-156">Leave **Automatically select hello certificate store[…]** checked and click **Next**.</span></span>
6. <span data-ttu-id="b2c7d-157">按一下 [完成] 和 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-157">Click **Finish** and **OK**.</span></span>

### <a name="upload-hello-pfx-file-toohello-cloud-service"></a><span data-ttu-id="b2c7d-158">上傳 hello PFX 檔案 toohello 雲端服務</span><span class="sxs-lookup"><span data-stu-id="b2c7d-158">Upload hello PFX file toohello cloud service</span></span>
1. <span data-ttu-id="b2c7d-159">移 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-159">Go toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b2c7d-160">選取 [雲端服務] 。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-160">Select **Cloud Services**.</span></span>
3. <span data-ttu-id="b2c7d-161">選取先前建立的 hello 分割/合併服務的 hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-161">Select hello cloud service you created above for hello Split/Merge service.</span></span>
4. <span data-ttu-id="b2c7d-162">按一下**憑證**hello 上方功能表上。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-162">Click **Certificates** on hello top menu.</span></span>
5. <span data-ttu-id="b2c7d-163">按一下**上傳**hello 下方列中。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-163">Click **Upload** in hello bottom bar.</span></span>
6. <span data-ttu-id="b2c7d-164">選取 hello PFX 檔案，然後輸入 hello 與上面相同的密碼。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-164">Select hello PFX file and enter hello same password as above.</span></span>
7. <span data-ttu-id="b2c7d-165">完成後，複製 hello hello 清單中的新項目中的 hello 憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-165">Once completed, copy hello certificate thumbprint from hello new entry in hello list.</span></span>

### <a name="update-hello-service-configuration-file"></a><span data-ttu-id="b2c7d-166">更新 hello 服務組態檔</span><span class="sxs-lookup"><span data-stu-id="b2c7d-166">Update hello service configuration file</span></span>
<span data-ttu-id="b2c7d-167">貼上上述複製 hello 指紋/value 屬性，這些設定的 hello 憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-167">Paste hello certificate thumbprint copied above into hello thumbprint/value attribute of these settings.</span></span>
<span data-ttu-id="b2c7d-168">Hello 背景工作角色：</span><span class="sxs-lookup"><span data-stu-id="b2c7d-168">For hello worker role:</span></span>
   ```
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="b2c7d-169">Hello web 角色：</span><span class="sxs-lookup"><span data-stu-id="b2c7d-169">For hello web role:</span></span>

   ```
    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />
    <Setting name="AllowedClientCertificateThumbprints" value="" />
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="b2c7d-170">請注意，不同的憑證應該用於 hello CA，來加密，生產環境部署的 hello 伺服器憑證和用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-170">Please note that for production deployments separate certificates should be used for hello CA, for encryption, hello Server certificate and client certificates.</span></span> <span data-ttu-id="b2c7d-171">如需詳細指示，請參閱 [安全性設定](sql-database-elastic-scale-split-merge-security-configuration.md)。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-171">For detailed instructions on this, see [Security Configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

## <a name="deploy-your-service"></a><span data-ttu-id="b2c7d-172">部署您的服務</span><span class="sxs-lookup"><span data-stu-id="b2c7d-172">Deploy your service</span></span>
1. <span data-ttu-id="b2c7d-173">移 toohello [Azure 入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-173">Go toohello [Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="b2c7d-174">按一下 hello**雲端服務**hello 左側索引標籤，選取您稍早建立的 hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-174">Click hello **Cloud Services** tab on hello left, and select hello cloud service that you created earlier.</span></span>
3. <span data-ttu-id="b2c7d-175">按一下 [儀表板] 。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-175">Click **Dashboard**.</span></span>
4. <span data-ttu-id="b2c7d-176">選擇 hello 預備環境，然後按一下**上傳新的預備環境部署**。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-176">Choose hello staging environment, then click **Upload a new staging deployment**.</span></span>
   
   ![預備][3]
5. <span data-ttu-id="b2c7d-178">在 [hello] 對話方塊中，輸入部署標籤。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-178">In hello dialog box, enter a deployment label.</span></span> <span data-ttu-id="b2c7d-179">「 封裝 」 和 「 設定 」 中，按一下 ' 從 Local'，然後選擇 hello **SplitMergeService.cspkg**檔案與您先前設定的.cscfg 檔案。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-179">For both 'Package' and 'Configuration', click 'From Local' and choose hello **SplitMergeService.cspkg** file and your .cscfg file that you configured earlier.</span></span>
6. <span data-ttu-id="b2c7d-180">請確定該 hello 核取方塊標示為**即使一個或多個角色包含單一執行個體部署**已核取。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-180">Ensure that hello checkbox labeled **Deploy even if one or more roles contain a single instance** is checked.</span></span>
7. <span data-ttu-id="b2c7d-181">叫用 hello 底部右 toobegin hello 部署中的 hello 刻度按鈕。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-181">Hit hello tick button in hello bottom right toobegin hello deployment.</span></span> <span data-ttu-id="b2c7d-182">預期 tootake 幾分鐘的時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-182">Expect it tootake a few minutes toocomplete.</span></span>

   ![上傳][4]

## <a name="troubleshoot-hello-deployment"></a><span data-ttu-id="b2c7d-184">疑難排解 hello 部署</span><span class="sxs-lookup"><span data-stu-id="b2c7d-184">Troubleshoot hello deployment</span></span>
<span data-ttu-id="b2c7d-185">如果您的 web 角色失敗 toocome 線上，可能是 hello 安全性組態有問題。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-185">If your web role fails toocome online, it is likely a problem with hello security configuration.</span></span> <span data-ttu-id="b2c7d-186">請檢查該 hello 上面所述，設定 SSL。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-186">Check that hello SSL is configured as described above.</span></span>

<span data-ttu-id="b2c7d-187">如果背景工作角色失敗 toocome 線上，但您的 web 角色會成功，則最有可能連接您稍早建立的 toohello 狀態資料庫時發生問題。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-187">If your worker role fails toocome online, but your web role succeeds, it is most likely a problem connecting toohello status database that you created earlier.</span></span>

* <span data-ttu-id="b2c7d-188">請確定您的.cscfg 中的 hello 連接字串正確無誤。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-188">Make sure that hello connection string in your .cscfg is accurate.</span></span>
* <span data-ttu-id="b2c7d-189">請檢查確定 hello 伺服器和資料庫存在，而且 hello 使用者識別碼和密碼正確無誤。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-189">Check that hello server and database exist, and that hello user id and password are correct.</span></span>
* <span data-ttu-id="b2c7d-190">Azure SQL db，hello 格式應該是 hello 連接字串：</span><span class="sxs-lookup"><span data-stu-id="b2c7d-190">For Azure SQL DB, hello connection string should be of hello form:</span></span>

   ```  
   Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
   ```

* <span data-ttu-id="b2c7d-191">請確定該 hello 伺服器名稱開頭不是**https://**。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-191">Ensure that hello server name does not begin with **https://**.</span></span>
* <span data-ttu-id="b2c7d-192">請確定您的 Azure SQL DB 伺服器允許 Azure 服務 tooconnect tooit。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-192">Ensure that your Azure SQL DB server allows Azure Services tooconnect tooit.</span></span> <span data-ttu-id="b2c7d-193">toodo，開啟 https://manage.windowsazure.com、 向左 hello 按一下 「 SQL 資料庫 」，在 hello 頂端，按一下 [伺服器] 然後選取您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-193">toodo this, open https://manage.windowsazure.com, click “SQL Databases” on hello left, click “Servers” at hello top, and select your server.</span></span> <span data-ttu-id="b2c7d-194">按一下**設定**在 hello 排名最前面，並確保該 hello **Azure 服務**設定為太"Yes"。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-194">Click **Configure** at hello top and ensure that hello **Azure Services** setting is set too“Yes”.</span></span> <span data-ttu-id="b2c7d-195">(請參閱 hello 必要條件 > 一節的這篇文章 hello 頂端)。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-195">(See hello Prerequisites section at hello top of this article).</span></span>

## <a name="test-hello-service-deployment"></a><span data-ttu-id="b2c7d-196">測試 hello 服務部署</span><span class="sxs-lookup"><span data-stu-id="b2c7d-196">Test hello service deployment</span></span>
### <a name="connect-with-a-web-browser"></a><span data-ttu-id="b2c7d-197">使用網頁瀏覽器連接</span><span class="sxs-lookup"><span data-stu-id="b2c7d-197">Connect with a web browser</span></span>
<span data-ttu-id="b2c7d-198">判斷您的分割合併服務的 hello web 端點。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-198">Determine hello web endpoint of your Split-Merge service.</span></span> <span data-ttu-id="b2c7d-199">您可以依移 toohello hello Azure 傳統入口網站中找到這**儀表板**您的雲端服務和下方**網站 URL** hello 右側。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-199">You can find this in hello Azure Classic Portal by going toohello **Dashboard** of your cloud service and looking under **Site URL** on hello right side.</span></span> <span data-ttu-id="b2c7d-200">取代**http://**與**https://**因為 hello 預設安全性設定停用 hello HTTP 端點。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-200">Replace **http://** with **https://** since hello default security settings disable hello HTTP endpoint.</span></span> <span data-ttu-id="b2c7d-201">此 url hello 頁面載入瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-201">Load hello page for this URL into your browser.</span></span>

### <a name="test-with-powershell-scripts"></a><span data-ttu-id="b2c7d-202">使用 PowerShell 指令碼進行測試</span><span class="sxs-lookup"><span data-stu-id="b2c7d-202">Test with PowerShell scripts</span></span>
<span data-ttu-id="b2c7d-203">hello 部署和您的環境，可以透過執行包含的 hello 範例 PowerShell 指令碼測試。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-203">hello deployment and your environment can be tested by running hello included sample PowerShell scripts.</span></span>

<span data-ttu-id="b2c7d-204">包含的 hello 指令碼檔案會：</span><span class="sxs-lookup"><span data-stu-id="b2c7d-204">hello script files included are:</span></span>

1. <span data-ttu-id="b2c7d-205">**SetupSampleSplitMergeEnvironment.ps1** - 設定分割/合併的測試資料層 (請參閱下表中的詳細說明)</span><span class="sxs-lookup"><span data-stu-id="b2c7d-205">**SetupSampleSplitMergeEnvironment.ps1** - sets up a test data tier for Split/Merge (see table below for detailed description)</span></span>
2. <span data-ttu-id="b2c7d-206">**ExecuteSampleSplitMerge.ps1** -hello 測試的測試作業會執行資料層 （請參閱下的表詳細說明）</span><span class="sxs-lookup"><span data-stu-id="b2c7d-206">**ExecuteSampleSplitMerge.ps1** - executes test operations on hello test data tier (see table below for detailed description)</span></span>
3. <span data-ttu-id="b2c7d-207">**GetMappings.ps1** -最上層的範例指令碼會列印出 hello 的 hello 分區對應的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-207">**GetMappings.ps1** - top-level sample script that prints out hello current state of hello shard mappings.</span></span>
4. <span data-ttu-id="b2c7d-208">**ShardManagement.psm1** -包裝的協助程式指令碼 hello ShardManagement 應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="b2c7d-208">**ShardManagement.psm1**  - helper script that wraps hello ShardManagement API</span></span>
5. <span data-ttu-id="b2c7d-209">**SqlDatabaseHelpers.psm1** - 用來建立及管理 SQL 資料庫的協助程式指令碼</span><span class="sxs-lookup"><span data-stu-id="b2c7d-209">**SqlDatabaseHelpers.psm1** - helper script for creating and managing SQL databases</span></span>
   
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="b2c7d-210">PowerShell 檔案</span><span class="sxs-lookup"><span data-stu-id="b2c7d-210">PowerShell file</span></span></th>
       <th><span data-ttu-id="b2c7d-211">步驟</span><span class="sxs-lookup"><span data-stu-id="b2c7d-211">Steps</span></span></th>
     </tr>
     <tr>
       <th rowspan="5"><span data-ttu-id="b2c7d-212">SetupSampleSplitMergeEnvironment.ps1</span><span class="sxs-lookup"><span data-stu-id="b2c7d-212">SetupSampleSplitMergeEnvironment.ps1</span></span></th>
       <td>1.    <span data-ttu-id="b2c7d-213">建立分區對應管理員資料庫</span><span class="sxs-lookup"><span data-stu-id="b2c7d-213">Creates a shard map manager database</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="b2c7d-214">建立 2 個分區資料庫。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-214">Creates 2 shard databases.</span></span>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="b2c7d-215">建立這些資料庫的分區對應 (刪除這些資料庫上的任何現有分區對應)。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-215">Creates a shard map for those database (deletes any existing shard maps on those databases).</span></span> </td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="b2c7d-216">在這兩個 hello 分區中, 建立小型範例資料表，並填入其中一種 hello 分區 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-216">Creates a small sample table in both hello shards, and populates hello table in one of hello shards.</span></span></td>
     </tr>
     <tr>
       <td>5.    <span data-ttu-id="b2c7d-217">宣告 hello SchemaInfo hello 分區化資料表。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-217">Declares hello SchemaInfo for hello sharded table.</span></span></td>
     </tr>
   </table>
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="b2c7d-218">PowerShell 檔案</span><span class="sxs-lookup"><span data-stu-id="b2c7d-218">PowerShell file</span></span></th>
       <th><span data-ttu-id="b2c7d-219">步驟</span><span class="sxs-lookup"><span data-stu-id="b2c7d-219">Steps</span></span></th>
     </tr>
   <tr>
       <th rowspan="4"><span data-ttu-id="b2c7d-220">ExecuteSampleSplitMerge.ps1</span><span class="sxs-lookup"><span data-stu-id="b2c7d-220">ExecuteSampleSplitMerge.ps1</span></span> </th>
       <td>1.    <span data-ttu-id="b2c7d-221">傳送的分割要求 toohello 分割合併服務 web 前端，可將來自 hello 第一個分區 toohello 第二個分區的一半 hello 資料分割。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-221">Sends a split request toohello Split-Merge Service web frontend, which splits half hello data from hello first shard toohello second shard.</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="b2c7d-222">輪詢 hello hello 分割要求的狀態並等待，直到完成 hello 要求的 web 前端。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-222">Polls hello web frontend for hello split request status and waits until hello request completes.</span></span></td>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="b2c7d-223">傳送的合併要求 toohello 分割合併服務 web 前端，將 hello 資料移從 hello 第二個分區後 toohello 第一個分區。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-223">Sends a merge request toohello Split-Merge Service web frontend, which moves hello data from hello second shard back toohello first shard.</span></span></td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="b2c7d-224">輪詢 hello web 前端的 hello 合併要求的狀態並等待直到 hello 要求完成為止。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-224">Polls hello web frontend for hello merge request status and waits until hello request completes.</span></span></td>
     </tr>
   </table>
   
## <a name="use-powershell-tooverify-your-deployment"></a><span data-ttu-id="b2c7d-225">使用 PowerShell tooverify 部署</span><span class="sxs-lookup"><span data-stu-id="b2c7d-225">Use PowerShell tooverify your deployment</span></span>
1. <span data-ttu-id="b2c7d-226">開啟新的 PowerShell 視窗並瀏覽 toohello 下載的目錄，hello 分割合併封裝，，然後瀏覽到 hello"powershell"目錄。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-226">Open a new PowerShell window and navigate toohello directory where you downloaded hello Split-Merge package, and then navigate into hello “powershell” directory.</span></span>
2. <span data-ttu-id="b2c7d-227">建立 Azure SQL database 伺服器 （或選擇現有的伺服器），將建立 hello 分區對應管理員和分區。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-227">Create an Azure SQL database server (or choose an existing server) where hello shard map manager and shards will be created.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b2c7d-228">hello SetupSampleSplitMergeEnvironment.ps1 指令碼會建立這些資料庫上 hello 預設 tookeep hello 指令碼簡單的同一部伺服器。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-228">hello SetupSampleSplitMergeEnvironment.ps1 script creates all these databases on hello same server by default tookeep hello script simple.</span></span> <span data-ttu-id="b2c7d-229">這不是限制的 hello 分割合併服務本身。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-229">This is not a restriction of hello Split-Merge Service itself.</span></span>
   >
   
   <span data-ttu-id="b2c7d-230">具有讀取/寫入存取 toohello hello 分割合併服務 toomove 資料和更新 hello 分區對應時需要資料庫的 SQL 驗證登入。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-230">A SQL authentication login with read/write access toohello DBs will be needed for hello Split-Merge service toomove data and update hello shard map.</span></span> <span data-ttu-id="b2c7d-231">Hello 分割合併服務是在 hello 雲端執行，因為它目前不支援整合式驗證。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-231">Since hello Split-Merge Service runs in hello cloud, it does not currently support Integrated Authentication.</span></span>
   
   <span data-ttu-id="b2c7d-232">請確定已 hello Azure SQL server tooallow hello IP 位址執行下列指令碼的 hello 機器的存取權。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-232">Make sure hello Azure SQL server is configured tooallow access from hello IP address of hello machine running these scripts.</span></span> <span data-ttu-id="b2c7d-233">您可以找到此設定下 hello Azure SQL server / 設定 / 允許的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-233">You can find this setting under hello Azure SQL server / configuration / allowed IP addresses.</span></span>
3. <span data-ttu-id="b2c7d-234">執行 hello SetupSampleSplitMergeEnvironment.ps1 指令碼 toocreate hello 範例環境。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-234">Execute hello SetupSampleSplitMergeEnvironment.ps1 script toocreate hello sample environment.</span></span>
   
   <span data-ttu-id="b2c7d-235">執行這個指令碼將會清除任何現有的分區對應管理資料結構上 hello 分區對應管理員資料庫與 hello 分區。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-235">Running this script will wipe out any existing shard map management data structures on hello shard map manager database and hello shards.</span></span> <span data-ttu-id="b2c7d-236">如果您希望 toore 初始化 hello 分區對應或分區，它可能會有用 toorerun hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-236">It may be useful toorerun hello script if you wish toore-initialize hello shard map or shards.</span></span>
   
   <span data-ttu-id="b2c7d-237">範例命令列：</span><span class="sxs-lookup"><span data-stu-id="b2c7d-237">Sample command line:</span></span>

   ```   
     .\SetupSampleSplitMergeEnvironment.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'
   ```      
4. <span data-ttu-id="b2c7d-238">Hello 範例環境中執行 hello Getmappings.ps1 指令碼 tooview hello 對應目前存在。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-238">Execute hello Getmappings.ps1 script tooview hello mappings that currently exist in hello sample environment.</span></span>
   
   ```
     .\GetMappings.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'

   ```         
5. <span data-ttu-id="b2c7d-239">Split 作業 （hello 第一個分區 toohello 第二個分區上移動半 hello 資料），然後合併作業 （hello 將資料移回至 hello 第一個分區），請執行 hello ExecuteSampleSplitMerge.ps1 指令碼 tooexecute。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-239">Execute hello ExecuteSampleSplitMerge.ps1 script tooexecute a split operation (moving half hello data on hello first shard toohello second shard) and then a merge operation (moving hello data back onto hello first shard).</span></span> <span data-ttu-id="b2c7d-240">如果您已設定 SSL 和左的 hello http 端點停用，請確定您改為使用 hello https:// 端點。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-240">If you configured SSL and left hello http endpoint disabled, ensure that you use hello https:// endpoint instead.</span></span>
   
   <span data-ttu-id="b2c7d-241">範例命令列：</span><span class="sxs-lookup"><span data-stu-id="b2c7d-241">Sample command line:</span></span>

   ```   
     .\ExecuteSampleSplitMerge.ps1
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net' 
         -SplitMergeServiceEndpoint 'https://mysplitmergeservice.cloudapp.net' 
         -CertificateThumbprint '0123456789abcdef0123456789abcdef01234567'
   ```      
   
   <span data-ttu-id="b2c7d-242">如果您收到錯誤的下方 hello，很可能是 Web 端點的憑證有問題。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-242">If you receive hello below error, it is most likely a problem with your Web endpoint’s certificate.</span></span> <span data-ttu-id="b2c7d-243">請嘗試 toohello Web 端點連接與您最愛的網頁瀏覽器，並檢查是否有憑證錯誤。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-243">Try connecting toohello Web endpoint with your favorite Web browser and check if there is a certificate error.</span></span>
   
     ```
     Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLSsecure channel.
     ```
   
   <span data-ttu-id="b2c7d-244">如果成功，hello 輸出看起來應該像下面的 hello:</span><span class="sxs-lookup"><span data-stu-id="b2c7d-244">If it succeeded, hello output should look like hello below:</span></span>
   
   ```
   > .\ExecuteSampleSplitMerge.ps1 -UserName 'mysqluser' -Password 'MySqlPassw0rd' -ShardMapManagerServerName 'abcdefghij.database.windows.net' -SplitMergeServiceEndpoint 'http://mysplitmergeservice.cloudapp.net' -CertificateThumbprint 0123456789abcdef0123456789abcdef01234567
   > Sending split request
   > Began split operation with id dc68dfa0-e22b-4823-886a-9bdc903c80f3
   > Polling split-merge request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Waiting for reference tables copy     completion.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > Sending merge request
   > Began merge operation with id 6ffc308f-d006-466b-b24e-857242ec5f66
   > Polling request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > 
   ```
6. <span data-ttu-id="b2c7d-245">試驗其他資料類型！</span><span class="sxs-lookup"><span data-stu-id="b2c7d-245">Experiment with other data types!</span></span> <span data-ttu-id="b2c7d-246">所有這些指令碼採用選擇性-ShardKeyType 參數，可讓您 toospecify hello 索引鍵類型。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-246">All of these scripts take an optional -ShardKeyType parameter that allows you toospecify hello key type.</span></span> <span data-ttu-id="b2c7d-247">hello 預設是 Int32，但您也可以指定 Int64、 Guid 或二進位檔。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-247">hello default is Int32, but you can also specify Int64, Guid, or Binary.</span></span>

## <a name="create-requests"></a><span data-ttu-id="b2c7d-248">建立要求</span><span class="sxs-lookup"><span data-stu-id="b2c7d-248">Create requests</span></span>
<span data-ttu-id="b2c7d-249">hello 服務可使用 hello web UI，或藉由匯入及使用 hello SplitMerge.psm1 PowerShell 模組會送出您的要求，透過 hello web 角色。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-249">hello service can be used either by using hello web UI or by importing and using hello SplitMerge.psm1 PowerShell module which will submit your requests through hello web role.</span></span>

<span data-ttu-id="b2c7d-250">hello 服務可以移動分區化資料表和參考資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-250">hello service can move data in both sharded tables and reference tables.</span></span> <span data-ttu-id="b2c7d-251">分區資料表具有分區化索引鍵資料行，且在每個分區上有不同的資料列資料。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-251">A sharded table has a sharding key column and has different row data on each shard.</span></span> <span data-ttu-id="b2c7d-252">參考資料表不是分區化使其包含 hello 相同資料上每個分區列資料。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-252">A reference table is not sharded so it contains hello same row data on every shard.</span></span> <span data-ttu-id="b2c7d-253">參考資料表適合用於不常變更，是使用的 tooJOIN 與查詢中的分區化資料表的資料。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-253">Reference tables are useful for data that does not change often and is used tooJOIN with sharded tables in queries.</span></span>

<span data-ttu-id="b2c7d-254">在訂單 tooperform 分割合併作業，您必須宣告 hello 分區化資料表和您想要移動的 toohave 的參考資料表。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-254">In order tooperform a split-merge operation, you must declare hello sharded tables and reference tables that you want toohave moved.</span></span> <span data-ttu-id="b2c7d-255">這是以 hello **SchemaInfo**應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-255">This is accomplished with hello **SchemaInfo** API.</span></span> <span data-ttu-id="b2c7d-256">這個 API 已在 hello **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema**命名空間。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-256">This API is in hello **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** namespace.</span></span>

1. <span data-ttu-id="b2c7d-257">針對每個分區化資料表建立**ShardedTableInfo**物件，描述 hello 資料表的父結構描述名稱 (選擇性，預設值太"dbo")、 hello 資料表名稱和 hello 包含 hello 分區化索引鍵的該資料表中的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-257">For each sharded table, create a **ShardedTableInfo** object describing hello table’s parent schema name (optional, defaults too“dbo”), hello table name, and hello column name in that table that contains hello sharding key.</span></span>
2. <span data-ttu-id="b2c7d-258">每個參考資料表中，建立**ReferenceTableInfo**物件，描述 hello 資料表的父結構描述名稱 (選擇性，預設值太"dbo") 和 hello 資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-258">For each reference table, create a **ReferenceTableInfo** object describing hello table’s parent schema name (optional, defaults too“dbo”) and hello table name.</span></span>
3. <span data-ttu-id="b2c7d-259">新增上述 TableInfo 物件 tooa 新 hello **SchemaInfo**物件。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-259">Add hello above TableInfo objects tooa new **SchemaInfo** object.</span></span>
4. <span data-ttu-id="b2c7d-260">取得參考 tooa **ShardMapManager**物件，並呼叫**GetSchemaInfoCollection**。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-260">Get a reference tooa **ShardMapManager** object, and call **GetSchemaInfoCollection**.</span></span>
5. <span data-ttu-id="b2c7d-261">新增 hello **SchemaInfo** toohello **SchemaInfoCollection**，提供 hello 分區對應名稱。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-261">Add hello **SchemaInfo** toohello **SchemaInfoCollection**, providing hello shard map name.</span></span>

<span data-ttu-id="b2c7d-262">Hello SetupSampleSplitMergeEnvironment.ps1 指令碼中可以看到此動作的範例。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-262">An example of this can be seen in hello SetupSampleSplitMergeEnvironment.ps1 script.</span></span>

<span data-ttu-id="b2c7d-263">hello 分割合併服務不會建立 hello 目標資料庫 （或 hello 資料庫中任何資料表的結構描述） 為您。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-263">hello Split-Merge service does not create hello target database (or schema for any tables in hello database) for you.</span></span> <span data-ttu-id="b2c7d-264">您必須預先建立傳送要求 toohello 服務之前。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-264">They must be pre-created before sending a request toohello service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b2c7d-265">疑難排解</span><span class="sxs-lookup"><span data-stu-id="b2c7d-265">Troubleshooting</span></span>
<span data-ttu-id="b2c7d-266">執行 hello 範例 powershell 指令碼時，您可能會看到下列訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="b2c7d-266">You may see hello below message when running hello sample powershell scripts:</span></span>

   ```
   Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLS secure channel.
   ```

<span data-ttu-id="b2c7d-267">此錯誤表示您的 SSL 憑證未正確設定。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-267">This error means that your SSL certificate is not configured correctly.</span></span> <span data-ttu-id="b2c7d-268">請依照 '連接的網頁瀏覽器' hello 一節中的指示。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-268">Please follow hello instructions in section 'Connecting with a web browser'.</span></span>

<span data-ttu-id="b2c7d-269">若無法提交要求，您可能會看到：</span><span class="sxs-lookup"><span data-stu-id="b2c7d-269">If you cannot submit requests you may see this:</span></span>

```
[Exception] System.Data.SqlClient.SqlException (0x80131904): Could not find stored procedure 'dbo.InsertRequest'. 
```

<span data-ttu-id="b2c7d-270">在此情況下，請檢查您的組態檔，在特定的 hello 設定**WorkerRoleSynchronizationStorageAccountConnectionString**。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-270">In this case, check your configuration file, in particular hello setting for **WorkerRoleSynchronizationStorageAccountConnectionString**.</span></span> <span data-ttu-id="b2c7d-271">此錯誤通常表示該 hello 背景工作角色無法順利初始化 hello 第一次使用的中繼資料資料庫。</span><span class="sxs-lookup"><span data-stu-id="b2c7d-271">This error typically indicates that hello worker role could not successfully initialize hello metadata database on first use.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/allowed-services.png
[2]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/manage.png
[3]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/staging.png
[4]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/upload.png
[5]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/storage.png

