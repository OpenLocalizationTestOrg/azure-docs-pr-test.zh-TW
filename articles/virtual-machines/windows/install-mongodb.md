---
title: "在 Azure 中的 Windows VM 上 MongoDB aaaInstall |Microsoft 文件"
description: "了解如何在執行 Windows Server 2012 R2 的 Azure VM 上 MongoDB tooinstall 建立 hello Resource Manager 部署模型。"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 53faf630-8da5-4955-8d0b-6e829bf30cba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: becd2c607d098e2bc806139e03f2c42f1f01f6f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="fcc52-103">在 Azure 中的 Windows VM 上安裝及設定 MongoDB</span><span class="sxs-lookup"><span data-stu-id="fcc52-103">Install and configure MongoDB on a Windows VM in Azure</span></span>
<span data-ttu-id="fcc52-104">[MongoDB](http://www.mongodb.org) 是受歡迎的高效能開放原始碼 NoSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="fcc52-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="fcc52-105">這篇文章會逐步引導您安裝和設定 Azure 中 Windows Server 2012 R2 虛擬機器 (VM) 上的 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="fcc52-105">This article guides you through installing and configuring MongoDB on a Windows Server 2012 R2 virtual machine (VM) in Azure.</span></span> <span data-ttu-id="fcc52-106">您也可以[在 Azure 中的 Linux VM 上安裝 MongoDB](../linux/install-mongodb.md)。</span><span class="sxs-lookup"><span data-stu-id="fcc52-106">You can also [install MongoDB on a Linux VM in Azure](../linux/install-mongodb.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fcc52-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="fcc52-107">Prerequisites</span></span>
<span data-ttu-id="fcc52-108">在安裝和設定 MongoDB 之前，您需要 toocreate VM，在理想情況下，加入資料磁碟 tooit。</span><span class="sxs-lookup"><span data-stu-id="fcc52-108">Before you install and configure MongoDB, you need toocreate a VM and, ideally, add a data disk tooit.</span></span> <span data-ttu-id="fcc52-109">請參閱下列文章 toocreate VM hello，並加入資料磁碟：</span><span class="sxs-lookup"><span data-stu-id="fcc52-109">See hello following articles toocreate a VM and add a data disk:</span></span>

* <span data-ttu-id="fcc52-110">建立 Windows Server VM 使用[hello Azure 入口網站](quick-create-portal.md)或[Azure PowerShell](quick-create-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="fcc52-110">Create a Windows Server VM using [hello Azure portal](quick-create-portal.md) or [Azure PowerShell](quick-create-powershell.md).</span></span>
* <span data-ttu-id="fcc52-111">附加資料磁碟 tooa Windows Server VM 使用[hello Azure 入口網站](attach-managed-disk-portal.md)或[Azure PowerShell](attach-disk-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="fcc52-111">Attach a data disk tooa Windows Server VM using [hello Azure portal](attach-managed-disk-portal.md) or [Azure PowerShell](attach-disk-ps.md).</span></span>

<span data-ttu-id="fcc52-112">安裝和設定 MongoDB，toobegin[登入 Windows Server VM tooyour](connect-logon.md)使用遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="fcc52-112">toobegin installing and configuring MongoDB, [log on tooyour Windows Server VM](connect-logon.md) by using Remote Desktop.</span></span>

## <a name="install-mongodb"></a><span data-ttu-id="fcc52-113">安裝 MongoDB</span><span class="sxs-lookup"><span data-stu-id="fcc52-113">Install MongoDB</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fcc52-114">MongoDB 安全性功能，例如驗證和 IP 位址繫結，均非預設為已啟用。</span><span class="sxs-lookup"><span data-stu-id="fcc52-114">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="fcc52-115">部署 MongoDB tooa 生產環境之前，應該啟用安全性功能。</span><span class="sxs-lookup"><span data-stu-id="fcc52-115">Security features should be enabled before deploying MongoDB tooa production environment.</span></span> <span data-ttu-id="fcc52-116">如需詳細資訊，請參閱 [MongoDB 安全性和驗證](http://www.mongodb.org/display/DOCS/Security+and+Authentication)。</span><span class="sxs-lookup"><span data-stu-id="fcc52-116">For more information, see [MongoDB Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>


1. <span data-ttu-id="fcc52-117">您已連接 tooyour 使用遠端桌面的 VM 之後，開啟 Internet Explorer 從 hello**啟動**hello VM 上的功能表。</span><span class="sxs-lookup"><span data-stu-id="fcc52-117">After you've connected tooyour VM using Remote Desktop, open Internet Explorer from hello **Start** menu on hello VM.</span></span>
2. <span data-ttu-id="fcc52-118">Internet Explorer 第一次開啟時，選取 [使用建議的安全性、隱私權與相容性設定]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="fcc52-118">Select **Use recommended security, privacy, and compatibility settings** when Internet Explorer first opens, and click **OK**.</span></span>
3. <span data-ttu-id="fcc52-119">預設會啟用 Internet Explorer 增強式安全性設定。</span><span class="sxs-lookup"><span data-stu-id="fcc52-119">Internet Explorer enhanced security configuration is enabled by default.</span></span> <span data-ttu-id="fcc52-120">新增允許的站台 hello MongoDB 網站 toohello 清單：</span><span class="sxs-lookup"><span data-stu-id="fcc52-120">Add hello MongoDB website toohello list of allowed sites:</span></span>
   
   * <span data-ttu-id="fcc52-121">選取 hello**工具**hello 右上角的圖示。</span><span class="sxs-lookup"><span data-stu-id="fcc52-121">Select hello **Tools** icon in hello upper-right corner.</span></span>
   * <span data-ttu-id="fcc52-122">在**網際網路選項**，選取 hello**安全性**索引標籤，然後選取 hello**信任的網站**圖示。</span><span class="sxs-lookup"><span data-stu-id="fcc52-122">In **Internet Options**, select hello **Security** tab, and then select hello **Trusted Sites** icon.</span></span>
   * <span data-ttu-id="fcc52-123">按一下 hello**網站** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fcc52-123">Click hello **Sites** button.</span></span> <span data-ttu-id="fcc52-124">新增*https://\*。 mongodb.org* toohello 份受信任的網站和 hello 然後關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="fcc52-124">Add *https://\*.mongodb.org* toohello list of trusted sites, and then close hello dialog box.</span></span>
     
     ![設定 Internet Explorer 安全性設定](./media/install-mongodb/configure-internet-explorer-security.png)
4. <span data-ttu-id="fcc52-126">瀏覽 toohello [MongoDB-下載](http://www.mongodb.org/downloads)頁面 (http://www.mongodb.org/downloads)。</span><span class="sxs-lookup"><span data-stu-id="fcc52-126">Browse toohello [MongoDB - Downloads](http://www.mongodb.org/downloads) page (http://www.mongodb.org/downloads).</span></span>
5. <span data-ttu-id="fcc52-127">如有需要選取 hello **Community 伺服器**版本，然後選取 hello 最新目前穩定版本及更新版本的 Windows Server 2008 R2 64 位元。</span><span class="sxs-lookup"><span data-stu-id="fcc52-127">If needed, select hello **Community Server** edition and then select hello latest current stable release for Windows Server 2008 R2 64-bit and later.</span></span> <span data-ttu-id="fcc52-128">toodownload hello 安裝程式中，按一下**下載 (msi)**。</span><span class="sxs-lookup"><span data-stu-id="fcc52-128">toodownload hello installer, click **DOWNLOAD (msi)**.</span></span>
   
    ![下載 MongoDB 安裝程式](./media/install-mongodb/download-mongodb.png)
   
    <span data-ttu-id="fcc52-130">Hello 下載完成之後，請執行 hello 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="fcc52-130">Run hello installer after hello download is complete.</span></span>
6. <span data-ttu-id="fcc52-131">閱讀並接受 hello 授權合約。</span><span class="sxs-lookup"><span data-stu-id="fcc52-131">Read and accept hello license agreement.</span></span> <span data-ttu-id="fcc52-132">當系統提示時，選取 [完整] 安裝。</span><span class="sxs-lookup"><span data-stu-id="fcc52-132">When you're prompted, select **Complete** install.</span></span>
7. <span data-ttu-id="fcc52-133">Hello 最後一個畫面上，按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="fcc52-133">On hello final screen, click **Install**.</span></span>

## <a name="configure-hello-vm-and-mongodb"></a><span data-ttu-id="fcc52-134">設定 hello VM 和 MongoDB</span><span class="sxs-lookup"><span data-stu-id="fcc52-134">Configure hello VM and MongoDB</span></span>
1. <span data-ttu-id="fcc52-135">hello MongoDB 安裝程式不會更新 hello 路徑變數。</span><span class="sxs-lookup"><span data-stu-id="fcc52-135">hello path variables are not updated by hello MongoDB installer.</span></span> <span data-ttu-id="fcc52-136">沒有 hello MongoDB `bin` path 變數中的位置，您需要 toospecify hello 完整路徑每次使用 MongoDB 的可執行檔。</span><span class="sxs-lookup"><span data-stu-id="fcc52-136">Without hello MongoDB `bin` location in your path variable, you need toospecify hello full path each time you use a MongoDB executable.</span></span> <span data-ttu-id="fcc52-137">tooadd hello 位置 tooyour path 變數：</span><span class="sxs-lookup"><span data-stu-id="fcc52-137">tooadd hello location tooyour path variable:</span></span>
   
   * <span data-ttu-id="fcc52-138">以滑鼠右鍵按一下 hello**啟動**功能表，然後選取**系統**。</span><span class="sxs-lookup"><span data-stu-id="fcc52-138">Right-click hello **Start** menu, and select **System**.</span></span>
   * <span data-ttu-id="fcc52-139">按一下 進階系統設定，然後按一下環境變數。</span><span class="sxs-lookup"><span data-stu-id="fcc52-139">Click **Advanced system settings**, and then click **Environment Variables**.</span></span>
   * <span data-ttu-id="fcc52-140">在 系統變數 底下，選取 路徑，然後按一下編輯。</span><span class="sxs-lookup"><span data-stu-id="fcc52-140">Under **System variables**, select **Path**, and then click **Edit**.</span></span>
     
     ![設定路徑變數](./media/install-mongodb/configure-path-variables.png)
     
     <span data-ttu-id="fcc52-142">新增 hello 路徑 tooyour MongoDB`bin`資料夾。</span><span class="sxs-lookup"><span data-stu-id="fcc52-142">Add hello path tooyour MongoDB `bin` folder.</span></span> <span data-ttu-id="fcc52-143">MongoDB 通常安裝在 C:\Program Files\MongoDB。</span><span class="sxs-lookup"><span data-stu-id="fcc52-143">MongoDB is typically installed in *C:\Program Files\MongoDB*.</span></span> <span data-ttu-id="fcc52-144">請確認 VM 上的 hello 安裝路徑。</span><span class="sxs-lookup"><span data-stu-id="fcc52-144">Verify hello installation path on your VM.</span></span> <span data-ttu-id="fcc52-145">hello 下列範例會將 hello 預設 MongoDB 安裝位置 toohello`PATH`變數：</span><span class="sxs-lookup"><span data-stu-id="fcc52-145">hello following example adds hello default MongoDB install location toohello `PATH` variable:</span></span>
     
     ```
     ;C:\Program Files\MongoDB\Server\3.2\bin
     ```
     
     > [!NOTE]
     > <span data-ttu-id="fcc52-146">要確定 tooadd hello 開頭的分號 (`;`) 您要新增位置 tooyour tooindicate`PATH`變數。</span><span class="sxs-lookup"><span data-stu-id="fcc52-146">Be sure tooadd hello leading semicolon (`;`) tooindicate that you are adding a location tooyour `PATH` variable.</span></span>

2. <span data-ttu-id="fcc52-147">在資料磁碟上建立 MongoDB 資料和記錄檔目錄。</span><span class="sxs-lookup"><span data-stu-id="fcc52-147">Create MongoDB data and log directories on your data disk.</span></span> <span data-ttu-id="fcc52-148">從 hello**啟動**功能表上，選取**命令提示字元**。</span><span class="sxs-lookup"><span data-stu-id="fcc52-148">From hello **Start** menu, select **Command Prompt**.</span></span> <span data-ttu-id="fcc52-149">下列範例中的 hello f： 磁碟機上建立 hello 目錄</span><span class="sxs-lookup"><span data-stu-id="fcc52-149">hello following examples create hello directories on drive F:</span></span>
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. <span data-ttu-id="fcc52-150">以下列命令，調整 hello 路徑 tooyour 資料 hello 開頭 MongoDB 執行個體，並據以記錄目錄：</span><span class="sxs-lookup"><span data-stu-id="fcc52-150">Start a MongoDB instance with hello following command, adjusting hello path tooyour data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    <span data-ttu-id="fcc52-151">它可能需要幾分鐘 MongoDB tooallocate hello 日誌檔案，並開始接聽連接。</span><span class="sxs-lookup"><span data-stu-id="fcc52-151">It may take several minutes for MongoDB tooallocate hello journal files and start listening for connections.</span></span> <span data-ttu-id="fcc52-152">所有的記錄訊息會導向的 toohello *F:\MongoLogs\mongolog.log*檔案做為`mongod.exe`啟動伺服器，並配置日誌檔案。</span><span class="sxs-lookup"><span data-stu-id="fcc52-152">All log messages are directed toohello *F:\MongoLogs\mongolog.log* file as `mongod.exe` server starts and allocates journal files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fcc52-153">hello 命令提示字元會保持專注在此工作上 MongoDB 執行個體正在執行時。</span><span class="sxs-lookup"><span data-stu-id="fcc52-153">hello command prompt stays focused on this task while your MongoDB instance is running.</span></span> <span data-ttu-id="fcc52-154">將保留 hello 命令提示字元視窗開啟 toocontinue 執行 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="fcc52-154">Leave hello command prompt window open toocontinue running MongoDB.</span></span> <span data-ttu-id="fcc52-155">或者，安裝 MongoDB 作為服務，hello 下一個步驟中所述。</span><span class="sxs-lookup"><span data-stu-id="fcc52-155">Or, install MongoDB as service, as detailed in hello next step.</span></span>

4. <span data-ttu-id="fcc52-156">為了更強固的 MongoDB 經驗，安裝 hello`mongod.exe`做為服務。</span><span class="sxs-lookup"><span data-stu-id="fcc52-156">For a more robust MongoDB experience, install hello `mongod.exe` as a service.</span></span> <span data-ttu-id="fcc52-157">建立服務，即表示您不需要 tooleave 執行每的次想 toouse MongoDB 的命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="fcc52-157">Creating a service means you don't need tooleave a command prompt running each time you want toouse MongoDB.</span></span> <span data-ttu-id="fcc52-158">建立 hello 服務，如下所示，據此調整 hello 路徑 tooyour 資料與記錄目錄：</span><span class="sxs-lookup"><span data-stu-id="fcc52-158">Create hello service as follows, adjusting hello path tooyour data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log `
        --logappend  --install
    ```
   
    <span data-ttu-id="fcc52-159">hello 前述的命令會建立稱為 MongoDB，「 Mongo DB 」 的描述。</span><span class="sxs-lookup"><span data-stu-id="fcc52-159">hello preceding command creates a service named MongoDB, with a description of "Mongo DB".</span></span> <span data-ttu-id="fcc52-160">也會指定下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="fcc52-160">hello following parameters are also specified:</span></span>
   
   * <span data-ttu-id="fcc52-161">hello`--dbpath`選項會指定 hello hello 資料目錄位置。</span><span class="sxs-lookup"><span data-stu-id="fcc52-161">hello `--dbpath` option specifies hello location of hello data directory.</span></span>
   * <span data-ttu-id="fcc52-162">hello`--logpath`選項必須是使用的 toospecify 記錄檔，因為 hello 執行中的服務並沒有命令視窗 toodisplay 輸出。</span><span class="sxs-lookup"><span data-stu-id="fcc52-162">hello `--logpath` option must be used toospecify a log file, because hello running service does not have a command window toodisplay output.</span></span>
   * <span data-ttu-id="fcc52-163">hello`--logappend`選項會指定 hello 服務重新啟動導致輸出 tooappend toohello 現有記錄檔。</span><span class="sxs-lookup"><span data-stu-id="fcc52-163">hello `--logappend` option specifies that a restart of hello service causes output tooappend toohello existing log file.</span></span>
   
   <span data-ttu-id="fcc52-164">toostart hello MongoDB 服務，請執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="fcc52-164">toostart hello MongoDB service, run hello following command:</span></span>
   
    ```
    net start MongoDB
    ```
   
    <span data-ttu-id="fcc52-165">如需建立 hello MongoDB 服務的詳細資訊，請參閱[設定 Windows 服務的 MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service)。</span><span class="sxs-lookup"><span data-stu-id="fcc52-165">For more information about creating hello MongoDB service, see [Configure a Windows Service for MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span></span>

## <a name="test-hello-mongodb-instance"></a><span data-ttu-id="fcc52-166">測試 hello MongoDB 執行個體</span><span class="sxs-lookup"><span data-stu-id="fcc52-166">Test hello MongoDB instance</span></span>
<span data-ttu-id="fcc52-167">當 MongoDB 執行為單一執行個體或安裝為服務，您現在可以開始建立和使用您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="fcc52-167">With MongoDB running as a single instance or installed as a service, you can now start creating and using your databases.</span></span> <span data-ttu-id="fcc52-168">toostart hello MongoDB 系統管理命令介面開啟另一個 [命令提示字元] 視窗，從 hello**啟動**功能表上，並輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="fcc52-168">toostart hello MongoDB administrative shell, open another command prompt window from hello **Start** menu, and enter hello following command:</span></span>

```
mongo  
```

<span data-ttu-id="fcc52-169">您可以列出 hello 資料庫以 hello`db`命令。</span><span class="sxs-lookup"><span data-stu-id="fcc52-169">You can list hello databases with hello `db` command.</span></span> <span data-ttu-id="fcc52-170">插入一些資料，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="fcc52-170">Insert some data as follows:</span></span>

```
db.foo.insert( { a : 1 } )
```

<span data-ttu-id="fcc52-171">搜尋資料，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="fcc52-171">Search for data as follows:</span></span>

```
db.foo.find()
```

<span data-ttu-id="fcc52-172">hello 輸出是 toohello 類似下列範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="fcc52-172">hello output is similar toohello following example:</span></span>

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

<span data-ttu-id="fcc52-173">結束 hello`mongo`主控台，如下所示：</span><span class="sxs-lookup"><span data-stu-id="fcc52-173">Exit hello `mongo` console as follows:</span></span>

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a><span data-ttu-id="fcc52-174">設定防火牆和網路安全性群組規則</span><span class="sxs-lookup"><span data-stu-id="fcc52-174">Configure firewall and Network Security Group rules</span></span>
<span data-ttu-id="fcc52-175">既然 MongoDB 已安裝且正在執行，連接埠 Windows 防火牆中開啟讓您可以從遠端連線 tooMongoDB。</span><span class="sxs-lookup"><span data-stu-id="fcc52-175">Now that MongoDB is installed and running, open a port in Windows Firewall so you can remotely connect tooMongoDB.</span></span> <span data-ttu-id="fcc52-176">toocreate 新增輸入的規則 tooallow TCP 連接埠 27017，開啟系統管理的 PowerShell 提示字元，並輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="fcc52-176">toocreate a new inbound rule tooallow TCP port 27017, open an administrative PowerShell prompt and enter hello following command:</span></span>

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

<span data-ttu-id="fcc52-177">您也可以建立 hello 規則使用 hello**具有進階安全性的 Windows 防火牆**圖形化管理工具。</span><span class="sxs-lookup"><span data-stu-id="fcc52-177">You can also create hello rule by using hello **Windows Firewall with Advanced Security** graphical management tool.</span></span> <span data-ttu-id="fcc52-178">建立新的輸入的規則 tooallow TCP 埠 27017。</span><span class="sxs-lookup"><span data-stu-id="fcc52-178">Create a new inbound rule tooallow TCP port 27017.</span></span>

<span data-ttu-id="fcc52-179">如有需要建立網路安全性群組規則 tooallow 存取 tooMongoDB 從外部 hello 現有的 Azure 虛擬網路子網路。</span><span class="sxs-lookup"><span data-stu-id="fcc52-179">If needed, create a Network Security Group rule tooallow access tooMongoDB from outside of hello existing Azure virtual network subnet.</span></span> <span data-ttu-id="fcc52-180">您可以建立 hello 網路安全性群組規則使用 hello [Azure 入口網站](nsg-quickstart-portal.md)或[Azure PowerShell](nsg-quickstart-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="fcc52-180">You can create hello Network Security Group rules by using hello [Azure portal](nsg-quickstart-portal.md) or [Azure PowerShell](nsg-quickstart-powershell.md).</span></span> <span data-ttu-id="fcc52-181">如同 hello Windows 防火牆規則，允許 TCP 連接埠 27017 toohello 的 MongoDB VM 的虛擬網路介面。</span><span class="sxs-lookup"><span data-stu-id="fcc52-181">As with hello Windows Firewall rules, allow TCP port 27017 toohello virtual network interface of your MongoDB VM.</span></span>

> [!NOTE]
> <span data-ttu-id="fcc52-182">TCP 連接埠 27017 是使用 MongoDB hello 預設通訊埠。</span><span class="sxs-lookup"><span data-stu-id="fcc52-182">TCP port 27017 is hello default port used by MongoDB.</span></span> <span data-ttu-id="fcc52-183">您可以變更此連接埠使用 hello`--port`參數啟動時`mongod.exe`以手動方式或從服務。</span><span class="sxs-lookup"><span data-stu-id="fcc52-183">You can change this port by using hello `--port` parameter when starting `mongod.exe` manually or from a service.</span></span> <span data-ttu-id="fcc52-184">如果您變更 hello 連接埠，請確定 tooupdate hello Windows 防火牆和網路安全性群組規則 hello 先前步驟中。</span><span class="sxs-lookup"><span data-stu-id="fcc52-184">If you change hello port, make sure tooupdate hello Windows Firewall and Network Security Group rules in hello preceding steps.</span></span>


## <a name="next-steps"></a><span data-ttu-id="fcc52-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fcc52-185">Next steps</span></span>
<span data-ttu-id="fcc52-186">在本教學課程中，您學到如何 tooinstall 和設定 Windows VM 上 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="fcc52-186">In this tutorial, you learned how tooinstall and configure MongoDB on your Windows VM.</span></span> <span data-ttu-id="fcc52-187">您現在可以存取 MongoDB 上您的 Windows VM，藉由下列進階主題 hello 中的 hello [MongoDB 文件](https://docs.mongodb.com/manual/)。</span><span class="sxs-lookup"><span data-stu-id="fcc52-187">You can now access MongoDB on your Windows VM, by following hello advanced topics in hello [MongoDB documentation](https://docs.mongodb.com/manual/).</span></span>

