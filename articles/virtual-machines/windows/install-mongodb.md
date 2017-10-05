---
title: "在 Azure 中 Windows 上安裝 MongoDB | Microsoft Docs"
description: "了解如何在 Azure VM (執行以 Resource Manager 部署範本建立的 Windows Server 2012 R2) 上安裝 MongoDB。"
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
ms.openlocfilehash: db1a550b9273925b304fe4280f2a1b0e115f856d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="eb8af-103">在 Azure 中的 Windows VM 上安裝及設定 MongoDB</span><span class="sxs-lookup"><span data-stu-id="eb8af-103">Install and configure MongoDB on a Windows VM in Azure</span></span>
<span data-ttu-id="eb8af-104">[MongoDB](http://www.mongodb.org) 是受歡迎的高效能開放原始碼 NoSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="eb8af-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="eb8af-105">這篇文章會逐步引導您安裝和設定 Azure 中 Windows Server 2012 R2 虛擬機器 (VM) 上的 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="eb8af-105">This article guides you through installing and configuring MongoDB on a Windows Server 2012 R2 virtual machine (VM) in Azure.</span></span> <span data-ttu-id="eb8af-106">您也可以[在 Azure 中的 Linux VM 上安裝 MongoDB](../linux/install-mongodb.md)。</span><span class="sxs-lookup"><span data-stu-id="eb8af-106">You can also [install MongoDB on a Linux VM in Azure](../linux/install-mongodb.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb8af-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="eb8af-107">Prerequisites</span></span>
<span data-ttu-id="eb8af-108">在安裝及設定 MongoDB 之前，您必須建立 VM，並且最好將資料磁碟新增至其中。</span><span class="sxs-lookup"><span data-stu-id="eb8af-108">Before you install and configure MongoDB, you need to create a VM and, ideally, add a data disk to it.</span></span> <span data-ttu-id="eb8af-109">請參閱下列文章，以建立 VM 並且新增資料磁碟︰</span><span class="sxs-lookup"><span data-stu-id="eb8af-109">See the following articles to create a VM and add a data disk:</span></span>

* <span data-ttu-id="eb8af-110">使用 [Azure 入口網站](quick-create-portal.md)或 [Azure PowerShell](quick-create-powershell.md) 建立 Windows Server VM。</span><span class="sxs-lookup"><span data-stu-id="eb8af-110">Create a Windows Server VM using [the Azure portal](quick-create-portal.md) or [Azure PowerShell](quick-create-powershell.md).</span></span>
* <span data-ttu-id="eb8af-111">使用 [Azure 入口網站](attach-managed-disk-portal.md)或 [Azure PowerShell](attach-disk-ps.md)將資料磁碟連結到 Windows Server VM。</span><span class="sxs-lookup"><span data-stu-id="eb8af-111">Attach a data disk to a Windows Server VM using [the Azure portal](attach-managed-disk-portal.md) or [Azure PowerShell](attach-disk-ps.md).</span></span>

<span data-ttu-id="eb8af-112">若要開始安裝和設定 MongoDB，請使用遠端桌面[登入您的 Windows Server VM](connect-logon.md)。</span><span class="sxs-lookup"><span data-stu-id="eb8af-112">To begin installing and configuring MongoDB, [log on to your Windows Server VM](connect-logon.md) by using Remote Desktop.</span></span>

## <a name="install-mongodb"></a><span data-ttu-id="eb8af-113">安裝 MongoDB</span><span class="sxs-lookup"><span data-stu-id="eb8af-113">Install MongoDB</span></span>
> [!IMPORTANT]
> <span data-ttu-id="eb8af-114">MongoDB 安全性功能，例如驗證和 IP 位址繫結，均非預設為已啟用。</span><span class="sxs-lookup"><span data-stu-id="eb8af-114">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="eb8af-115">安全性功能應該在將 MongoDB 部署到生產環境前加以啟用。</span><span class="sxs-lookup"><span data-stu-id="eb8af-115">Security features should be enabled before deploying MongoDB to a production environment.</span></span> <span data-ttu-id="eb8af-116">如需詳細資訊，請參閱 [MongoDB 安全性和驗證](http://www.mongodb.org/display/DOCS/Security+and+Authentication)。</span><span class="sxs-lookup"><span data-stu-id="eb8af-116">For more information, see [MongoDB Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>


1. <span data-ttu-id="eb8af-117">使用遠端桌面連線到 VM 之後，請從 VM 上的 [開始] 功能表開啟 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="eb8af-117">After you've connected to your VM using Remote Desktop, open Internet Explorer from the **Start** menu on the VM.</span></span>
2. <span data-ttu-id="eb8af-118">Internet Explorer 第一次開啟時，選取 [使用建議的安全性、隱私權與相容性設定]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="eb8af-118">Select **Use recommended security, privacy, and compatibility settings** when Internet Explorer first opens, and click **OK**.</span></span>
3. <span data-ttu-id="eb8af-119">預設會啟用 Internet Explorer 增強式安全性設定。</span><span class="sxs-lookup"><span data-stu-id="eb8af-119">Internet Explorer enhanced security configuration is enabled by default.</span></span> <span data-ttu-id="eb8af-120">將 MongoDB 網站新增至允許的網站清單︰</span><span class="sxs-lookup"><span data-stu-id="eb8af-120">Add the MongoDB website to the list of allowed sites:</span></span>
   
   * <span data-ttu-id="eb8af-121">選取右上方的 [工具] 圖示。</span><span class="sxs-lookup"><span data-stu-id="eb8af-121">Select the **Tools** icon in the upper-right corner.</span></span>
   * <span data-ttu-id="eb8af-122">在 [網際網路選項] 中，選取 [安全性] 索引標籤，然後選取 [受信任的網站] 圖示。</span><span class="sxs-lookup"><span data-stu-id="eb8af-122">In **Internet Options**, select the **Security** tab, and then select the **Trusted Sites** icon.</span></span>
   * <span data-ttu-id="eb8af-123">按一下 [網站] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="eb8af-123">Click the **Sites** button.</span></span> <span data-ttu-id="eb8af-124">將 *https://\*.mongodb.org* 新增至受信任的網站清單，然後關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="eb8af-124">Add *https://\*.mongodb.org* to the list of trusted sites, and then close the dialog box.</span></span>
     
     ![設定 Internet Explorer 安全性設定](./media/install-mongodb/configure-internet-explorer-security.png)
4. <span data-ttu-id="eb8af-126">瀏覽至 [MongoDB - 下載](http://www.mongodb.org/downloads)頁面 (http://www.mongodb.org/downloads)。</span><span class="sxs-lookup"><span data-stu-id="eb8af-126">Browse to the [MongoDB - Downloads](http://www.mongodb.org/downloads) page (http://www.mongodb.org/downloads).</span></span>
5. <span data-ttu-id="eb8af-127">如果需要，選取 **Community Server** 版本，然後選取目前最新的穩定版本 Windows Server 2008 R2 64 位元和更新版本。</span><span class="sxs-lookup"><span data-stu-id="eb8af-127">If needed, select the **Community Server** edition and then select the latest current stable release for Windows Server 2008 R2 64-bit and later.</span></span> <span data-ttu-id="eb8af-128">若要下載安裝程式，請按一下 [下載 (msi)]。</span><span class="sxs-lookup"><span data-stu-id="eb8af-128">To download the installer, click **DOWNLOAD (msi)**.</span></span>
   
    ![下載 MongoDB 安裝程式](./media/install-mongodb/download-mongodb.png)
   
    <span data-ttu-id="eb8af-130">下載完成之後，請執行安裝程式。</span><span class="sxs-lookup"><span data-stu-id="eb8af-130">Run the installer after the download is complete.</span></span>
6. <span data-ttu-id="eb8af-131">閱讀並接受授權合約。</span><span class="sxs-lookup"><span data-stu-id="eb8af-131">Read and accept the license agreement.</span></span> <span data-ttu-id="eb8af-132">當系統提示時，選取 [完整] 安裝。</span><span class="sxs-lookup"><span data-stu-id="eb8af-132">When you're prompted, select **Complete** install.</span></span>
7. <span data-ttu-id="eb8af-133">在最後畫面上，按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="eb8af-133">On the final screen, click **Install**.</span></span>

## <a name="configure-the-vm-and-mongodb"></a><span data-ttu-id="eb8af-134">設定 VM 和 MongoDB</span><span class="sxs-lookup"><span data-stu-id="eb8af-134">Configure the VM and MongoDB</span></span>
1. <span data-ttu-id="eb8af-135">路徑變數不會被 MongoDB 安裝程式更新。</span><span class="sxs-lookup"><span data-stu-id="eb8af-135">The path variables are not updated by the MongoDB installer.</span></span> <span data-ttu-id="eb8af-136">在您的路徑變數中沒有 MongoDB `bin` 位置，您必須在每次使用 MongoDB 可執行檔時指定完整路徑。</span><span class="sxs-lookup"><span data-stu-id="eb8af-136">Without the MongoDB `bin` location in your path variable, you need to specify the full path each time you use a MongoDB executable.</span></span> <span data-ttu-id="eb8af-137">若要將位置新增至路徑變數︰</span><span class="sxs-lookup"><span data-stu-id="eb8af-137">To add the location to your path variable:</span></span>
   
   * <span data-ttu-id="eb8af-138">使用滑鼠右鍵按一下 [開始] 功能表，然後選取 [系統]。</span><span class="sxs-lookup"><span data-stu-id="eb8af-138">Right-click the **Start** menu, and select **System**.</span></span>
   * <span data-ttu-id="eb8af-139">按一下 [進階系統設定]，然後按一下 [環境變數]。</span><span class="sxs-lookup"><span data-stu-id="eb8af-139">Click **Advanced system settings**, and then click **Environment Variables**.</span></span>
   * <span data-ttu-id="eb8af-140">在 [系統變數] 底下，選取 [路徑]，然後按一下 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="eb8af-140">Under **System variables**, select **Path**, and then click **Edit**.</span></span>
     
     ![設定路徑變數](./media/install-mongodb/configure-path-variables.png)
     
     <span data-ttu-id="eb8af-142">將路徑新增至您的 MongoDB `bin` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="eb8af-142">Add the path to your MongoDB `bin` folder.</span></span> <span data-ttu-id="eb8af-143">MongoDB 通常安裝在 C:\Program Files\MongoDB。</span><span class="sxs-lookup"><span data-stu-id="eb8af-143">MongoDB is typically installed in *C:\Program Files\MongoDB*.</span></span> <span data-ttu-id="eb8af-144">請確認您的 VM 上的安裝路徑。</span><span class="sxs-lookup"><span data-stu-id="eb8af-144">Verify the installation path on your VM.</span></span> <span data-ttu-id="eb8af-145">下列範例會將預設 MongoDB 安裝位置新增至 `PATH` 變數︰</span><span class="sxs-lookup"><span data-stu-id="eb8af-145">The following example adds the default MongoDB install location to the `PATH` variable:</span></span>
     
     ```
     ;C:\Program Files\MongoDB\Server\3.2\bin
     ```
     
     > [!NOTE]
     > <span data-ttu-id="eb8af-146">請務必新增開頭分號 (`;`) 來指出您要將位置新增至 `PATH` 變數。</span><span class="sxs-lookup"><span data-stu-id="eb8af-146">Be sure to add the leading semicolon (`;`) to indicate that you are adding a location to your `PATH` variable.</span></span>

2. <span data-ttu-id="eb8af-147">在資料磁碟上建立 MongoDB 資料和記錄檔目錄。</span><span class="sxs-lookup"><span data-stu-id="eb8af-147">Create MongoDB data and log directories on your data disk.</span></span> <span data-ttu-id="eb8af-148">在 [開始] 功能表中，選取 [命令提示字元]。</span><span class="sxs-lookup"><span data-stu-id="eb8af-148">From the **Start** menu, select **Command Prompt**.</span></span> <span data-ttu-id="eb8af-149">下列範例會在磁碟機 F: 上建立目錄</span><span class="sxs-lookup"><span data-stu-id="eb8af-149">The following examples create the directories on drive F:</span></span>
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. <span data-ttu-id="eb8af-150">以下列命令啟動 MongoDB 執行個體，並且據以調整您的資料和記錄檔目錄︰</span><span class="sxs-lookup"><span data-stu-id="eb8af-150">Start a MongoDB instance with the following command, adjusting the path to your data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    <span data-ttu-id="eb8af-151">MongoDB 可能需要花費數分鐘來配置日誌檔案，並開始接聽連線。</span><span class="sxs-lookup"><span data-stu-id="eb8af-151">It may take several minutes for MongoDB to allocate the journal files and start listening for connections.</span></span> <span data-ttu-id="eb8af-152">在 `mongod.exe` 伺服器啟動和配置日誌檔案時，所有記錄訊息都會傳送至 *F:\MongoLogs\mongolog.log* 檔案。</span><span class="sxs-lookup"><span data-stu-id="eb8af-152">All log messages are directed to the *F:\MongoLogs\mongolog.log* file as `mongod.exe` server starts and allocates journal files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="eb8af-153">當您的 MongoDB 執行個體正在執行時，命令提示字元會專注於這項工作。</span><span class="sxs-lookup"><span data-stu-id="eb8af-153">The command prompt stays focused on this task while your MongoDB instance is running.</span></span> <span data-ttu-id="eb8af-154">保持命令提示字元視窗開啟以繼續執行 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="eb8af-154">Leave the command prompt window open to continue running MongoDB.</span></span> <span data-ttu-id="eb8af-155">或者，安裝 MongoDB 做為服務，如下一個步驟所述。</span><span class="sxs-lookup"><span data-stu-id="eb8af-155">Or, install MongoDB as service, as detailed in the next step.</span></span>

4. <span data-ttu-id="eb8af-156">為了更穩固的 MongoDB 體驗，請安裝 `mongod.exe` 做為服務。</span><span class="sxs-lookup"><span data-stu-id="eb8af-156">For a more robust MongoDB experience, install the `mongod.exe` as a service.</span></span> <span data-ttu-id="eb8af-157">建立服務表示您不需要在每次想要使用 MongoDB 時都保持命令提示字元執行。</span><span class="sxs-lookup"><span data-stu-id="eb8af-157">Creating a service means you don't need to leave a command prompt running each time you want to use MongoDB.</span></span> <span data-ttu-id="eb8af-158">如下所示建立服務，據以調整您的資料和記錄檔目錄的路徑︰</span><span class="sxs-lookup"><span data-stu-id="eb8af-158">Create the service as follows, adjusting the path to your data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log `
        --logappend  --install
    ```
   
    <span data-ttu-id="eb8af-159">上述命令會建立一個名為 MongoDB 的服務，其說明為 "Mongo DB"。</span><span class="sxs-lookup"><span data-stu-id="eb8af-159">The preceding command creates a service named MongoDB, with a description of "Mongo DB".</span></span> <span data-ttu-id="eb8af-160">同時指定下列參數：</span><span class="sxs-lookup"><span data-stu-id="eb8af-160">The following parameters are also specified:</span></span>
   
   * <span data-ttu-id="eb8af-161">`--dbpath` 選項指出資料目錄的位置。</span><span class="sxs-lookup"><span data-stu-id="eb8af-161">The `--dbpath` option specifies the location of the data directory.</span></span>
   * <span data-ttu-id="eb8af-162">`--logpath` 選項必須用來指定記錄檔，因為執行中的服務沒有命令視窗可以顯示輸出。</span><span class="sxs-lookup"><span data-stu-id="eb8af-162">The `--logpath` option must be used to specify a log file, because the running service does not have a command window to display output.</span></span>
   * <span data-ttu-id="eb8af-163">`--logappend` 選項指出重新啟動服務會導致輸出附加在現有的記錄檔案中。</span><span class="sxs-lookup"><span data-stu-id="eb8af-163">The `--logappend` option specifies that a restart of the service causes output to append to the existing log file.</span></span>
   
   <span data-ttu-id="eb8af-164">若要啟動 MongoDB 服務，請執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="eb8af-164">To start the MongoDB service, run the following command:</span></span>
   
    ```
    net start MongoDB
    ```
   
    <span data-ttu-id="eb8af-165">如需建立 MongoDB 服務的詳細資訊，請參閱[設定 MongoDB 的 Windows 服務](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service)。</span><span class="sxs-lookup"><span data-stu-id="eb8af-165">For more information about creating the MongoDB service, see [Configure a Windows Service for MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span></span>

## <a name="test-the-mongodb-instance"></a><span data-ttu-id="eb8af-166">測試 MongoDB 執行個體</span><span class="sxs-lookup"><span data-stu-id="eb8af-166">Test the MongoDB instance</span></span>
<span data-ttu-id="eb8af-167">當 MongoDB 執行為單一執行個體或安裝為服務，您現在可以開始建立和使用您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="eb8af-167">With MongoDB running as a single instance or installed as a service, you can now start creating and using your databases.</span></span> <span data-ttu-id="eb8af-168">要啟動 MongoDB 管理殼層，請從 [開始] 功能表中開啟另一個命令提示字元視窗，並輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="eb8af-168">To start the MongoDB administrative shell, open another command prompt window from the **Start** menu, and enter the following command:</span></span>

```
mongo  
```

<span data-ttu-id="eb8af-169">您可以使用 `db` 命令列出資料庫。</span><span class="sxs-lookup"><span data-stu-id="eb8af-169">You can list the databases with the `db` command.</span></span> <span data-ttu-id="eb8af-170">插入一些資料，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="eb8af-170">Insert some data as follows:</span></span>

```
db.foo.insert( { a : 1 } )
```

<span data-ttu-id="eb8af-171">搜尋資料，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="eb8af-171">Search for data as follows:</span></span>

```
db.foo.find()
```

<span data-ttu-id="eb8af-172">輸出類似於下列範例：</span><span class="sxs-lookup"><span data-stu-id="eb8af-172">The output is similar to the following example:</span></span>

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

<span data-ttu-id="eb8af-173">結束 `mongo` 主控台，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="eb8af-173">Exit the `mongo` console as follows:</span></span>

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a><span data-ttu-id="eb8af-174">設定防火牆和網路安全性群組規則</span><span class="sxs-lookup"><span data-stu-id="eb8af-174">Configure firewall and Network Security Group rules</span></span>
<span data-ttu-id="eb8af-175">現在，MongoDB 已安裝並正在執行，在 Windows 防火牆中開啟一個連接埠，才能遠端連線至 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="eb8af-175">Now that MongoDB is installed and running, open a port in Windows Firewall so you can remotely connect to MongoDB.</span></span> <span data-ttu-id="eb8af-176">若要建立新的輸入規則以允許 TCP 連接埠 27017，開啟系統管理 PowerShell 提示字元並輸入下列命令︰</span><span class="sxs-lookup"><span data-stu-id="eb8af-176">To create a new inbound rule to allow TCP port 27017, open an administrative PowerShell prompt and enter the following command:</span></span>

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

<span data-ttu-id="eb8af-177">您也可以使用**具有進階安全性的 Windows 防火牆** 圖形化管理工具來建立規則。</span><span class="sxs-lookup"><span data-stu-id="eb8af-177">You can also create the rule by using the **Windows Firewall with Advanced Security** graphical management tool.</span></span> <span data-ttu-id="eb8af-178">建立新的輸入規則以允許 TCP 連接埠 27017。</span><span class="sxs-lookup"><span data-stu-id="eb8af-178">Create a new inbound rule to allow TCP port 27017.</span></span>

<span data-ttu-id="eb8af-179">如有需要，建立網路安全性群組規則以允許從現有 Azure 虛擬網路子網路外部存取 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="eb8af-179">If needed, create a Network Security Group rule to allow access to MongoDB from outside of the existing Azure virtual network subnet.</span></span> <span data-ttu-id="eb8af-180">您可以使用 [Azure 入口網站](nsg-quickstart-portal.md) 或 [Azure PowerShell](nsg-quickstart-powershell.md) 來建立網路安全性群組規則。</span><span class="sxs-lookup"><span data-stu-id="eb8af-180">You can create the Network Security Group rules by using the [Azure portal](nsg-quickstart-portal.md) or [Azure PowerShell](nsg-quickstart-powershell.md).</span></span> <span data-ttu-id="eb8af-181">如同 Windows 防火牆規則，允許 TCP 連接埠 27017 連接至 MongoDB VM 的虛擬網路介面。</span><span class="sxs-lookup"><span data-stu-id="eb8af-181">As with the Windows Firewall rules, allow TCP port 27017 to the virtual network interface of your MongoDB VM.</span></span>

> [!NOTE]
> <span data-ttu-id="eb8af-182">TCP 連接埠 27017 是 MongoDB 使用的預設連接埠。</span><span class="sxs-lookup"><span data-stu-id="eb8af-182">TCP port 27017 is the default port used by MongoDB.</span></span> <span data-ttu-id="eb8af-183">您可以在手動啟動或從服務啟動 `mongod.exe` 時，使用 `--port` 參數變更此連接埠。</span><span class="sxs-lookup"><span data-stu-id="eb8af-183">You can change this port by using the `--port` parameter when starting `mongod.exe` manually or from a service.</span></span> <span data-ttu-id="eb8af-184">如果您變更連接埠，請確定在先前步驟中更新 Windows 防火牆和網路安全性群組規則。</span><span class="sxs-lookup"><span data-stu-id="eb8af-184">If you change the port, make sure to update the Windows Firewall and Network Security Group rules in the preceding steps.</span></span>


## <a name="next-steps"></a><span data-ttu-id="eb8af-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eb8af-185">Next steps</span></span>
<span data-ttu-id="eb8af-186">在本教學課程中，您了解如何在 Windows VM 上安裝及設定 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="eb8af-186">In this tutorial, you learned how to install and configure MongoDB on your Windows VM.</span></span> <span data-ttu-id="eb8af-187">您現在可以遵循 [MongoDB 文件](https://docs.mongodb.com/manual/) 中的進階主題，以便存取 Windows VM 上的 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="eb8af-187">You can now access MongoDB on your Windows VM, by following the advanced topics in the [MongoDB documentation](https://docs.mongodb.com/manual/).</span></span>

