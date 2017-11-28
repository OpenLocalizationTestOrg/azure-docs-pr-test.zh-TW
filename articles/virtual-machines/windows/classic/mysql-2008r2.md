---
title: "aaaCreate 傳統的 Azure VM 執行 MySQL |Microsoft 文件"
description: "建立 Azure 虛擬機器執行 Windows Server 2012 R2 和 hello 使用 hello 傳統部署模型的 MySQL 資料庫。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 98fa06d2-9b92-4d05-ac16-3f8e9fd4feaa
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: cynthn
ms.openlocfilehash: 2c9564955c2bab197a8e494e939ce16c0b9bb605
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-mysql-on-a-virtual-machine-created-with-hello-classic-deployment-model-running-windows-server-2016"></a><span data-ttu-id="f6256-103">在執行 Windows Server 2016 的 hello 傳統部署模型所建立的虛擬機器上安裝 MySQL</span><span class="sxs-lookup"><span data-stu-id="f6256-103">Install MySQL on a virtual machine created with hello classic deployment model running Windows Server 2016</span></span>
<span data-ttu-id="f6256-104">[MySQL](https://www.mysql.com) 是一種很受歡迎的開放原始碼 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="f6256-104">[MySQL](https://www.mysql.com) is a popular open source, SQL database.</span></span> <span data-ttu-id="f6256-105">本教學課程示範如何 tooinstall 和執行 hello**社群版本的 MySQL 5.7.18**為 MySQL 伺服器上執行的虛擬機器**Windows Server 2016**。</span><span class="sxs-lookup"><span data-stu-id="f6256-105">This tutorial shows you how tooinstall and run hello **community version of MySQL 5.7.18** as a MySQL Server on a virtual machine running **Windows Server 2016**.</span></span> <span data-ttu-id="f6256-106">對於非 MySQL 或 Windows Server 的版本，操作方式可能略有不同。</span><span class="sxs-lookup"><span data-stu-id="f6256-106">Your experience might be slightly different for other versions of MySQL or Windows Server.</span></span>

<span data-ttu-id="f6256-107">如需 MySQL 安裝在 Linux 上的指示，請參閱：[如何在 Azure 上 MySQL tooinstall](../../linux/mysql-install.md)。</span><span class="sxs-lookup"><span data-stu-id="f6256-107">For instructions on installing MySQL on Linux, refer to: [How tooinstall MySQL on Azure](../../linux/mysql-install.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f6256-108">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="f6256-108">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f6256-109">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="f6256-109">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="f6256-110">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="f6256-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

## <a name="create-a-virtual-machine-running-windows-server-2016"></a><span data-ttu-id="f6256-111">建立執行 Windows Server 2016 的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="f6256-111">Create a virtual machine running Windows Server 2016</span></span>
<span data-ttu-id="f6256-112">如果您還沒有執行 Windows Server 2016 的 VM，您可以使用這個[教學課程](./tutorial.md)toocreate hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f6256-112">If you don't already have a VM running Windows Server 2016, you can use this [tutorial](./tutorial.md) toocreate hello virtual machine.</span></span>

## <a name="attach-a-data-disk"></a><span data-ttu-id="f6256-113">連接資料磁碟</span><span class="sxs-lookup"><span data-stu-id="f6256-113">Attach a data disk</span></span>
<span data-ttu-id="f6256-114">Hello 虛擬機器建立之後，您可以選擇性地附加資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="f6256-114">After hello virtual machine is created, you can optionally attach a data disk.</span></span> <span data-ttu-id="f6256-115">新增資料磁碟建議用於生產工作負載和 tooavoid hello 作業系統磁碟機 （c:） 上的空間用盡，包括 hello 作業系統。</span><span class="sxs-lookup"><span data-stu-id="f6256-115">Adding a data disk is recommended for production workloads and tooavoid running out of space on hello OS drive (C:), which includes hello operating system.</span></span>

<span data-ttu-id="f6256-116">請參閱[tooattach 資料磁碟 tooa Windows 虛擬機器如何](../attach-managed-disk-portal.md)依照 hello 指示連接空磁碟。</span><span class="sxs-lookup"><span data-stu-id="f6256-116">See [How tooattach a data disk tooa Windows virtual machine](../attach-managed-disk-portal.md) and follow hello instructions for attaching an empty disk.</span></span> <span data-ttu-id="f6256-117">設定 hello 主機快取設定太**無**或**唯讀**。</span><span class="sxs-lookup"><span data-stu-id="f6256-117">Set hello host cache setting too**None** or **Read-only**.</span></span>

## <a name="log-on-toohello-virtual-machine"></a><span data-ttu-id="f6256-118">登入 toohello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="f6256-118">Log on toohello virtual machine</span></span>
<span data-ttu-id="f6256-119">接下來，您將[登入 toohello 虛擬機器](./connect-logon.md)，才能安裝 MySQL。</span><span class="sxs-lookup"><span data-stu-id="f6256-119">Next, you'll [log on toohello virtual machine](./connect-logon.md) so you can install MySQL.</span></span>

## <a name="install-and-run-mysql-community-server-on-hello-virtual-machine"></a><span data-ttu-id="f6256-120">安裝並執行 hello 虛擬機器上的 MySQL Community 伺服器</span><span class="sxs-lookup"><span data-stu-id="f6256-120">Install and run MySQL Community Server on hello virtual machine</span></span>
<span data-ttu-id="f6256-121">請遵循這些步驟 tooinstall、 設定及執行的 MySQL Server hello 社群版本：</span><span class="sxs-lookup"><span data-stu-id="f6256-121">Follow these steps tooinstall, configure, and run hello Community version of MySQL Server:</span></span>

> [!NOTE]
> <span data-ttu-id="f6256-122">當下載使用 Internet Explorer 的項目，您可以設定 hello IE**增強式安全性設定**tooOff，並簡化 hello 下載程序。</span><span class="sxs-lookup"><span data-stu-id="f6256-122">When downloading items using Internet Explorer, you can set hello IE **Enhanced Security Configuration** tooOff, and simplify hello downloading process.</span></span> <span data-ttu-id="f6256-123">從 hello 開始 功能表，按一下 系統管理工具/伺服器管理員/本機伺服器，然後按一下 IE**增強式安全性設定**並設定 hello 組態 tooOff)。</span><span class="sxs-lookup"><span data-stu-id="f6256-123">From hello Start menu, click Administrative Tools/Server Manager/Local Server, then click IE **Enhanced Security Configuration** and set hello configuration tooOff).</span></span>
>
>

1. <span data-ttu-id="f6256-124">您已連接 toohello 虛擬機器使用遠端桌面之後，請按一下**Internet Explorer**從 hello [開始] 畫面。</span><span class="sxs-lookup"><span data-stu-id="f6256-124">After you've connected toohello virtual machine using Remote Desktop, click **Internet Explorer** from hello start screen.</span></span>
2. <span data-ttu-id="f6256-125">選取 hello**工具**按鈕在 hello 右上角 （hello cogged 的滾輪圖示），然後按一下**網際網路選項**。</span><span class="sxs-lookup"><span data-stu-id="f6256-125">Select hello **Tools** button in hello upper-right corner (hello cogged wheel icon), and then click **Internet Options**.</span></span> <span data-ttu-id="f6256-126">按一下 hello**安全性**索引標籤上，按一下 hello**信任的網站**圖示，然後按一下hello**網站** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f6256-126">Click hello **Security** tab, click hello **Trusted Sites** icon, and then click hello **Sites** button.</span></span> <span data-ttu-id="f6256-127">新增信任的網站 http://*.mysql.com toohello 清單。</span><span class="sxs-lookup"><span data-stu-id="f6256-127">Add http://*.mysql.com toohello list of trusted sites.</span></span> <span data-ttu-id="f6256-128">按一下 關閉，然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="f6256-128">Click **Close**, and then click **OK**.</span></span>
3. <span data-ttu-id="f6256-129">在 hello 位址列的 Internet Explorer 中，輸入 https://dev.mysql.com/downloads/mysql/。</span><span class="sxs-lookup"><span data-stu-id="f6256-129">In hello address bar of Internet Explorer, type https://dev.mysql.com/downloads/mysql/.</span></span>
4. <span data-ttu-id="f6256-130">使用 hello MySQL 網站 toolocate 並下載 hello hello MySQL Windows 安裝程式最新版本。</span><span class="sxs-lookup"><span data-stu-id="f6256-130">Use hello MySQL site toolocate and download hello latest version of hello MySQL Installer for Windows.</span></span> <span data-ttu-id="f6256-131">在選擇 hello MySQL 安裝程式時，下載已完成檔案組 (例如，hello mysql-安裝程式-社群-5.7.18.0.msi 352.8 MB 的檔案大小)，並儲存 hello installer hello 的 hello 版本。</span><span class="sxs-lookup"><span data-stu-id="f6256-131">When choosing hello MySQL Installer, download hello version that has hello complete file set (for example, hello mysql-installer-community-5.7.18.0.msi with a file size of 352.8 MB), and save hello installer.</span></span>
5. <span data-ttu-id="f6256-132">當下載完成 hello 安裝程式之後時，按一下 **執行**toolaunch 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="f6256-132">When hello installer has finished downloading, click **Run** toolaunch setup.</span></span>
6. <span data-ttu-id="f6256-133">在 hello**合約**頁面上，接受 hello 授權合約，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="f6256-133">On hello **License Agreement** page, accept hello license agreement and click **Next**.</span></span>
7. <span data-ttu-id="f6256-134">在 hello**選擇安裝類型**頁面上，按一下 hello 安裝類型，然後再按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="f6256-134">On hello **Choosing a Setup Type** page, click hello setup type that you want, and then click **Next**.</span></span> <span data-ttu-id="f6256-135">hello 下列步驟假設 hello 選取範圍的 hello**僅限伺服器**安裝類型。</span><span class="sxs-lookup"><span data-stu-id="f6256-135">hello following steps assume hello selection of hello **Server only** setup type.</span></span>
8. <span data-ttu-id="f6256-136">如果 hello**檢查需求**顯示頁面上，按一下**Execute** toolet hello 安裝程式會安裝任何遺漏的元件。</span><span class="sxs-lookup"><span data-stu-id="f6256-136">If hello **Check Requirements** page displays, click **Execute** toolet hello installer install any missing components.</span></span> <span data-ttu-id="f6256-137">請遵循顯示，例如 hello c + + 可轉散發套件的執行階段的任何指示。</span><span class="sxs-lookup"><span data-stu-id="f6256-137">Follow any instructions that display, such as hello C++ Redistributable runtime.</span></span>
9. <span data-ttu-id="f6256-138">在 hello**安裝**頁面上，按一下**Execute**。</span><span class="sxs-lookup"><span data-stu-id="f6256-138">On hello **Installation** page, click **Execute**.</span></span> <span data-ttu-id="f6256-139">安裝完成時，按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="f6256-139">When installation is complete, click **Next**.</span></span>

10. <span data-ttu-id="f6256-140">在 hello**產品組態**頁面上，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="f6256-140">On hello **Product Configuration** page, click **Next**.</span></span>

11. <span data-ttu-id="f6256-141">在 hello**類型和網路**頁面上，指定所需的組態類型和連接選項，包括 hello TCP 連接埠，如有需要。</span><span class="sxs-lookup"><span data-stu-id="f6256-141">On hello **Type and Networking** page, specify your desired configuration type and connectivity options, including hello TCP port if needed.</span></span> <span data-ttu-id="f6256-142">選取 [顯示進階選項]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="f6256-142">Select **Show Advanced Options**, and then click **Next**.</span></span>
    ![](./media/mysql-2008r2/MySQL_TypeNetworking.png)

12. <span data-ttu-id="f6256-143">在 hello**帳戶和角色**頁面上，指定強式 MySQL 根密碼。</span><span class="sxs-lookup"><span data-stu-id="f6256-143">On hello **Accounts and Roles** page, specify a strong MySQL root password.</span></span> <span data-ttu-id="f6256-144">視需要新增其他 MySQL 使用者帳戶，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="f6256-144">Add additional MySQL user accounts as needed, and then click **Next**.</span></span>

    ![](./media/mysql-2008r2/MySQL_AccountsRoles_Filled.png)
13. <span data-ttu-id="f6256-145">在 hello **Windows 服務**頁面上，執行 hello MySQL 伺服器當做 Windows 服務，如有需要指定變更 toohello 預設設定，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="f6256-145">On hello **Windows Service** page, specify changes toohello default settings for running hello MySQL Server as a Windows service as needed, and then click **Next**.</span></span>

    ![](./media/mysql-2008r2/MySQL_WindowsService.png)
14. <span data-ttu-id="f6256-146">hello hello 上的選擇**增益集和擴充功能**是選擇性的頁面。</span><span class="sxs-lookup"><span data-stu-id="f6256-146">hello choices on hello **Plugins and Extensions** page are optional.</span></span> <span data-ttu-id="f6256-147">按一下**下一步**toocontinue。</span><span class="sxs-lookup"><span data-stu-id="f6256-147">Click **Next** toocontinue.</span></span>
15. <span data-ttu-id="f6256-148">在 hello**進階選項**頁面上，視需要指定變更 toologging 選項，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="f6256-148">On hello **Advanced Options** page, specify changes toologging options as needed, and then click **Next**.</span></span>

    ![](./media/mysql-2008r2/MySQL_AdvOptions.png)
16. <span data-ttu-id="f6256-149">在 hello**套用伺服器設定**頁面上，按一下**Execute**。</span><span class="sxs-lookup"><span data-stu-id="f6256-149">On hello **Apply Server Configuration** page, click **Execute**.</span></span> <span data-ttu-id="f6256-150">Hello 組態步驟完成時，按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="f6256-150">When hello configuration steps are complete, click **Finish**.</span></span>
17. <span data-ttu-id="f6256-151">在 hello**產品組態**頁面上，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="f6256-151">On hello **Product Configuration** page, click **Next**.</span></span>
18. <span data-ttu-id="f6256-152">在 hello**安裝完成**頁面上，按一下**複製記錄 tooClipboard**如果它在更新版本中，然後再按一下想要 tooexamine**完成**。</span><span class="sxs-lookup"><span data-stu-id="f6256-152">On hello **Installation Complete** page, click **Copy Log tooClipboard** if you want tooexamine it later, and then click **Finish**.</span></span>
19. <span data-ttu-id="f6256-153">從 hello [開始] 畫面，輸入**mysql**，然後按一下 **MySQL 5.7 命令列用戶端**。</span><span class="sxs-lookup"><span data-stu-id="f6256-153">From hello start screen, type **mysql**, and then click **MySQL 5.7 Command-Line Client**.</span></span>
20. <span data-ttu-id="f6256-154">輸入您在步驟 12 中指定的 hello 根密碼，然後您會看到提示，您可以在其中發出命令 tooconfigure MySQL。</span><span class="sxs-lookup"><span data-stu-id="f6256-154">Enter hello root password that you specified in step 12 and you are presented with a prompt where you can issue commands tooconfigure MySQL.</span></span> <span data-ttu-id="f6256-155">Hello 命令和語法的詳細資訊，請參閱[MySQL 參考手冊](https://dev.mysql.com/doc/refman/5.7/en/server-configuration.html)。</span><span class="sxs-lookup"><span data-stu-id="f6256-155">For hello details of commands and syntax, see [MySQL Reference Manuals](https://dev.mysql.com/doc/refman/5.7/en/server-configuration.html).</span></span>

    ![](./media/mysql-2008r2/MySQL_CommandPrompt.png)
21. <span data-ttu-id="f6256-156">您也可以設定伺服器預設設定，例如基底 hello 和資料目錄以及磁碟機。</span><span class="sxs-lookup"><span data-stu-id="f6256-156">You can also configure server configuration default settings, such as hello base and data directories and drives.</span></span> <span data-ttu-id="f6256-157">如需詳細資訊，請參閱 [6.1.2 伺服器組態預設值](https://dev.mysql.com/doc/refman/5.7/en/server-configuration-defaults.html)。</span><span class="sxs-lookup"><span data-stu-id="f6256-157">For more information, see [6.1.2 Server Configuration Defaults](https://dev.mysql.com/doc/refman/5.7/en/server-configuration-defaults.html).</span></span>

## <a name="configure-endpoints"></a><span data-ttu-id="f6256-158">設定端點</span><span class="sxs-lookup"><span data-stu-id="f6256-158">Configure endpoints</span></span>

<span data-ttu-id="f6256-159">Hello MySQL 服務 toobe 可用 tooclient 電腦 hello 網際網路上，您必須設定 hello TCP 連接埠的端點，並建立 Windows 防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="f6256-159">For hello MySQL service toobe available tooclient computers on hello Internet, you must configure an endpoint for hello TCP port and create a Windows Firewall rule.</span></span> <span data-ttu-id="f6256-160">hello 的 hello MySQL Server 服務所接聽的 MySQL 用戶端的預設通訊埠值為 3306。</span><span class="sxs-lookup"><span data-stu-id="f6256-160">hello default port value on which hello MySQL Server service listens for MySQL clients is 3306.</span></span> <span data-ttu-id="f6256-161">您可以指定另一個連接埠，只要 hello 連接埠與 hello hello 上提供的值一致**類型和網路**頁面 （hello 上一個程序的步驟 11）。</span><span class="sxs-lookup"><span data-stu-id="f6256-161">You can specify another port, as long as hello port is consistent with hello value supplied on hello **Type and Networking** page (step 11 of hello previous procedure).</span></span>

> [!NOTE]
> <span data-ttu-id="f6256-162">用於實際執行環境，請考慮讓 hello MySQL 伺服器 hello 網際網路上的服務可用 tooall 電腦的安全性含意 hello。</span><span class="sxs-lookup"><span data-stu-id="f6256-162">For production use, consider hello security implications of making hello MySQL Server service available tooall computers on hello Internet.</span></span> <span data-ttu-id="f6256-163">您可以定義 hello 組允許 toouse hello 端點的存取控制清單 (ACL) 的來源 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f6256-163">You can define hello set of source IP addresses that are allowed toouse hello endpoint with an Access Control List (ACL).</span></span> <span data-ttu-id="f6256-164">如需詳細資訊，請參閱[如何 tooSet 端點 tooa 虛擬機器](setup-endpoints.md)。</span><span class="sxs-lookup"><span data-stu-id="f6256-164">For more information, see [How tooSet Up Endpoints tooa Virtual Machine](setup-endpoints.md).</span></span>
>
>

<span data-ttu-id="f6256-165">tooconfigure hello MySQL Server 服務的端點：</span><span class="sxs-lookup"><span data-stu-id="f6256-165">tooconfigure an endpoint for hello MySQL Server service:</span></span>

1. <span data-ttu-id="f6256-166">在 hello Azure 入口網站，按一下 **虛擬機器 （傳統）**，按一下 MySQL 虛擬機器的 hello 名稱，然後按一下**端點**。</span><span class="sxs-lookup"><span data-stu-id="f6256-166">In hello Azure portal, click **Virtual Machines (classic)**, click hello name of your MySQL virtual machine, and then click **Endpoints**.</span></span>
2. <span data-ttu-id="f6256-167">Hello 命令列中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="f6256-167">In hello command bar, click **Add**.</span></span>
3. <span data-ttu-id="f6256-168">在 hello**加入端點**頁面上，輸入唯一的名稱**名稱**。</span><span class="sxs-lookup"><span data-stu-id="f6256-168">On hello **Add endpoint** page, type a unique name for **Name**.</span></span>
4. <span data-ttu-id="f6256-169">選取**TCP**做為 hello 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="f6256-169">Select **TCP** as hello protocol.</span></span>
5. <span data-ttu-id="f6256-170">輸入 hello 通訊埠編號，例如**3306**，在這兩**公用連接埠**和**私用連接埠**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="f6256-170">Type hello port number, such as **3306**, in both **Public Port** and **Private Port**, and then click **OK**.</span></span>

## <a name="add-a-windows-firewall-rule-tooallow-mysql-traffic"></a><span data-ttu-id="f6256-171">加入 Windows 防火牆規則 tooallow MySQL 流量</span><span class="sxs-lookup"><span data-stu-id="f6256-171">Add a Windows Firewall rule tooallow MySQL traffic</span></span>
<span data-ttu-id="f6256-172">Windows 防火牆規則，允許從 hello 網際網路上，執行下列命令在 hello MySQL 流量 tooadd_提升權限的 Windows PowerShell 命令提示字元_hello MySQL server 虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="f6256-172">tooadd a Windows Firewall rule that allows MySQL traffic from hello Internet, run hello following command at an _elevated Windows PowerShell command prompt_ on hello MySQL server virtual machine.</span></span>

    New-NetFirewallRule -DisplayName "MySQL57" -Direction Inbound –Protocol TCP –LocalPort 3306 -Action Allow -Profile Public

## <a name="test-your-remote-connection"></a><span data-ttu-id="f6256-173">測試您的遠端連線</span><span class="sxs-lookup"><span data-stu-id="f6256-173">Test your remote connection</span></span>
<span data-ttu-id="f6256-174">tootest 您遠端連線 toohello Azure VM 執行 hello MySQL 伺服器服務，您必須提供 hello 包含 hello VN hello 雲端服務 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="f6256-174">tootest your remote connection toohello Azure VM running hello MySQL Server service, you must provide hello DNS name of hello cloud service containing hello VN.</span></span>

1. <span data-ttu-id="f6256-175">在 hello Azure 入口網站，按一下 **虛擬機器 （傳統）**，按一下 MySQL server 虛擬機器，hello 名稱，然後按一下**概觀**。</span><span class="sxs-lookup"><span data-stu-id="f6256-175">In hello Azure portal, click **Virtual Machines (classic)**, click hello name of your MySQL server virtual machine, and then click **Overview**.</span></span>
2. <span data-ttu-id="f6256-176">從 hello 虛擬機器儀表板，請注意 hello **DNS 名稱**值。</span><span class="sxs-lookup"><span data-stu-id="f6256-176">From hello virtual machine dashboard, note hello **DNS Name** value.</span></span> <span data-ttu-id="f6256-177">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="f6256-177">Here is an example:</span></span>

   ![](media/mysql-2008r2/MySQL_DNSName.png)
3. <span data-ttu-id="f6256-178">從本機電腦上執行的 MySQL 或 hello MySQL 用戶端，執行下列中的 MySQL 使用者身分的命令 toolog hello。</span><span class="sxs-lookup"><span data-stu-id="f6256-178">From a local computer running MySQL or hello MySQL client, run hello following command toolog in as a MySQL user.</span></span>

     <span data-ttu-id="f6256-179">mysql -u <yourMysqlUsername> -p -h <yourDNSname></span><span class="sxs-lookup"><span data-stu-id="f6256-179">mysql -u <yourMysqlUsername> -p -h <yourDNSname></span></span>

   <span data-ttu-id="f6256-180">例如，使用 hello MySQL 使用者名稱_dbadmin3_和 hello _testmysql.cloudapp.net_ DNS 名稱 hello 虛擬機器，您可以開始使用下列命令的 hello MySQL:</span><span class="sxs-lookup"><span data-stu-id="f6256-180">For example, using hello MySQL user name _dbadmin3_ and hello _testmysql.cloudapp.net_ DNS name for hello virtual machine, you could start MySQL using hello following command:</span></span>

     <span data-ttu-id="f6256-181">mysql -u dbadmin3 -p -h testmysql.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="f6256-181">mysql -u dbadmin3 -p -h testmysql.cloudapp.net</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6256-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f6256-182">Next steps</span></span>
<span data-ttu-id="f6256-183">toolearn 有關執行 MySQL 的詳細資訊，請參閱 「 hello [MySQL 文件](http://dev.mysql.com/doc/)。</span><span class="sxs-lookup"><span data-stu-id="f6256-183">toolearn more about running MySQL, see hello [MySQL Documentation](http://dev.mysql.com/doc/).</span></span>
