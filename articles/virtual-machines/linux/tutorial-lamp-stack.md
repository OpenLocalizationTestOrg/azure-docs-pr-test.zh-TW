---
title: "在 Azure 中 Linux 虛擬機器上的燈 aaaDeploy |Microsoft 文件"
description: "教學課程-在 Azure 中的 Linux VM 上安裝 hello LAMP 堆疊"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/03/2017
ms.author: danlep
ms.openlocfilehash: a3d0ecb3277f15bd0a2fdc0d85b738a760e68865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-lamp-web-server-on-an-azure-vm"></a><span data-ttu-id="a6252-103">在 Azure VM 上安裝 LAMP 網頁伺服器</span><span class="sxs-lookup"><span data-stu-id="a6252-103">Install a LAMP web server on an Azure VM</span></span>
<span data-ttu-id="a6252-104">本文將告訴您如何 toodeploy Apache web 伺服器、 MySQL 和 Ubuntu VM 在 Azure 上的 PHP （hello LAMP 堆疊）。</span><span class="sxs-lookup"><span data-stu-id="a6252-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="a6252-105">如果您偏好 hello NGINX 網頁伺服器，請參閱 hello [LEMP 堆疊](tutorial-lemp-stack.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="a6252-105">If you prefer hello NGINX web server, see hello [LEMP stack](tutorial-lemp-stack.md) tutorial.</span></span> <span data-ttu-id="a6252-106">toosee hello 燈伺服器在動作中，您可以選擇性地安裝和設定 WordPress 網站。</span><span class="sxs-lookup"><span data-stu-id="a6252-106">toosee hello LAMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="a6252-107">在本教學課程中，您了解如何：</span><span class="sxs-lookup"><span data-stu-id="a6252-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a6252-108">建立 Ubuntu VM (hello LAMP 堆疊中的 hello 'L')</span><span class="sxs-lookup"><span data-stu-id="a6252-108">Create an Ubuntu VM (hello 'L' in hello LAMP stack)</span></span>
> * <span data-ttu-id="a6252-109">針對 Web 流量開啟連接埠 80</span><span class="sxs-lookup"><span data-stu-id="a6252-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="a6252-110">安裝 Apache、MySQL 和 PHP</span><span class="sxs-lookup"><span data-stu-id="a6252-110">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="a6252-111">驗證安裝和設定</span><span class="sxs-lookup"><span data-stu-id="a6252-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="a6252-112">Hello 燈伺服器上安裝 WordPress</span><span class="sxs-lookup"><span data-stu-id="a6252-112">Install WordPress on hello LAMP server</span></span>


<span data-ttu-id="a6252-113">如需 hello LAMP 堆疊，包括建議的生產環境，請參閱 hello [Ubuntu 文件](https://help.ubuntu.com/community/ApacheMySQLPHP)。</span><span class="sxs-lookup"><span data-stu-id="a6252-113">For more on hello LAMP stack, including recommendations for a production environment, see hello [Ubuntu documentation](https://help.ubuntu.com/community/ApacheMySQLPHP).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a6252-114">如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="a6252-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="a6252-115">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="a6252-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a6252-116">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="a6252-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-apache-mysql-and-php"></a><span data-ttu-id="a6252-117">安裝 Apache、MySQL 和 PHP</span><span class="sxs-lookup"><span data-stu-id="a6252-117">Install Apache, MySQL, and PHP</span></span>

<span data-ttu-id="a6252-118">執行下列命令 tooupdate Ubuntu 封裝來源的 hello 並安裝 Apache、 MySQL 和 PHP。</span><span class="sxs-lookup"><span data-stu-id="a6252-118">Run hello following command tooupdate Ubuntu package sources and install Apache, MySQL, and PHP.</span></span> <span data-ttu-id="a6252-119">請注意結尾 hello hello 命令 hello 插入號 (^)。</span><span class="sxs-lookup"><span data-stu-id="a6252-119">Note hello caret (^) at hello end of hello command.</span></span>


```bash
sudo apt update && sudo apt install lamp-server^
```



<span data-ttu-id="a6252-120">您會提示的 tooinstall hello 套件以及其他相依性。</span><span class="sxs-lookup"><span data-stu-id="a6252-120">You are prompted tooinstall hello packages and other dependencies.</span></span> <span data-ttu-id="a6252-121">出現提示時，設定根密碼 MySQL，然後 [Enter] toocontinue。</span><span class="sxs-lookup"><span data-stu-id="a6252-121">When prompted, set a root password for MySQL, and then [Enter] toocontinue.</span></span> <span data-ttu-id="a6252-122">請遵循其餘提示 hello。</span><span class="sxs-lookup"><span data-stu-id="a6252-122">Follow hello remaining prompts.</span></span> <span data-ttu-id="a6252-123">此程序會 hello 最小必要的 PHP 延伸模組需要 toouse PHP 安裝 MySQL。</span><span class="sxs-lookup"><span data-stu-id="a6252-123">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![MySQL 根密碼頁面][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="a6252-125">驗證安裝和設定</span><span class="sxs-lookup"><span data-stu-id="a6252-125">Verify installation and configuration</span></span>


### <a name="apache"></a><span data-ttu-id="a6252-126">Apache</span><span class="sxs-lookup"><span data-stu-id="a6252-126">Apache</span></span>

<span data-ttu-id="a6252-127">核取 hello 版本的 Apache 以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="a6252-127">Check hello version of Apache with hello following command:</span></span>
```bash
apache2 -v
```

<span data-ttu-id="a6252-128">Apache 安裝，且連接埠 80 開啟 tooyour VM、 hello web 伺服器現在可以從 hello 存取網際網路。</span><span class="sxs-lookup"><span data-stu-id="a6252-128">With Apache installed, and port 80 open tooyour VM, hello web server can now be accessed from hello internet.</span></span> <span data-ttu-id="a6252-129">tooview hello Apache2 Ubuntu 預設頁面上，開啟網頁瀏覽器，並輸入 hello VM 的 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a6252-129">tooview hello Apache2 Ubuntu Default Page, open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="a6252-130">使用 hello 用 tooSSH toohello VM 公用 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="a6252-130">Use hello public IP address you used tooSSH toohello VM:</span></span>

![Apache 預設網頁][3]


### <a name="mysql"></a><span data-ttu-id="a6252-132">MySQL</span><span class="sxs-lookup"><span data-stu-id="a6252-132">MySQL</span></span>

<span data-ttu-id="a6252-133">以下列命令的 hello 檢查 hello MySQL 版本 (請注意 hello 資本`V`參數):</span><span class="sxs-lookup"><span data-stu-id="a6252-133">Check hello version of MySQL with hello following command (note hello capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="a6252-134">我們建議您執行下列指令碼 toohelp 安全 hello 安裝 MySQL hello:</span><span class="sxs-lookup"><span data-stu-id="a6252-134">We recommend running hello following script toohelp secure hello installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="a6252-135">輸入 MySQL 根密碼，並設定您的環境的 hello 安全性設定。</span><span class="sxs-lookup"><span data-stu-id="a6252-135">Enter your MySQL root password, and configure hello security settings for your environment.</span></span>

<span data-ttu-id="a6252-136">如果您想 toocreate MySQL 資料庫，新增使用者，或變更組態設定，登入 tooMySQL:</span><span class="sxs-lookup"><span data-stu-id="a6252-136">If you want toocreate a MySQL database, add users, or change configuration settings, login tooMySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="a6252-137">當完成時，結束 hello mysql 提示字元中輸入`\q`。</span><span class="sxs-lookup"><span data-stu-id="a6252-137">When done, exit hello mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="a6252-138">PHP</span><span class="sxs-lookup"><span data-stu-id="a6252-138">PHP</span></span>

<span data-ttu-id="a6252-139">核取 hello 版本的 PHP 以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="a6252-139">Check hello version of PHP with hello following command:</span></span>

```bash
php -v
```

<span data-ttu-id="a6252-140">如果您想進一步 tootest，建立快速的 PHP 資訊頁面 tooview 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="a6252-140">If you want tootest further, create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="a6252-141">hello，下列命令會建立 hello PHP 資訊頁面：</span><span class="sxs-lookup"><span data-stu-id="a6252-141">hello following command creates hello PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```

<span data-ttu-id="a6252-142">現在您可以檢查您所建立的 hello PHP 資訊頁面。</span><span class="sxs-lookup"><span data-stu-id="a6252-142">Now you can check hello PHP info page you created.</span></span> <span data-ttu-id="a6252-143">開啟瀏覽器並移過`http://yourPublicIPAddress/info.php`。</span><span class="sxs-lookup"><span data-stu-id="a6252-143">Open a browser and go too`http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="a6252-144">取代您的 VM hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a6252-144">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="a6252-145">它看起來應該類似 toothis 映像。</span><span class="sxs-lookup"><span data-stu-id="a6252-145">It should look similar toothis image.</span></span>

![PHP 資訊網頁][2]

[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]


## <a name="next-steps"></a><span data-ttu-id="a6252-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a6252-147">Next steps</span></span>

<span data-ttu-id="a6252-148">在本教學課程中，您已在 Azure 中部署 LAMP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="a6252-148">In this tutorial, you deployed a LAMP server in Azure.</span></span> <span data-ttu-id="a6252-149">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="a6252-149">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a6252-150">建立 Ubuntu VM</span><span class="sxs-lookup"><span data-stu-id="a6252-150">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="a6252-151">針對 Web 流量開啟連接埠 80</span><span class="sxs-lookup"><span data-stu-id="a6252-151">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="a6252-152">安裝 Apache、MySQL 和 PHP</span><span class="sxs-lookup"><span data-stu-id="a6252-152">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="a6252-153">驗證安裝和設定</span><span class="sxs-lookup"><span data-stu-id="a6252-153">Verify installation and configuration</span></span>
> * <span data-ttu-id="a6252-154">Hello 燈伺服器上安裝 WordPress</span><span class="sxs-lookup"><span data-stu-id="a6252-154">Install WordPress on hello LAMP server</span></span>

<span data-ttu-id="a6252-155">如何前進 toohello 下一個教學課程 toolearn toosecure 網頁伺服器使用 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="a6252-155">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a6252-156">使用 SSL 保護網路伺服器</span><span class="sxs-lookup"><span data-stu-id="a6252-156">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lamp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lamp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lamp-stack/apachesuccesspage.png