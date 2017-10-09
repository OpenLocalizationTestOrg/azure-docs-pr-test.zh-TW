---
title: "在 Azure 中 Linux 虛擬機器上的 aaaDeploy LEMP |Microsoft 文件"
description: "教學課程-在 Azure 中的 Linux VM 上安裝 hello LEMP 堆疊"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/03/2017
ms.author: danlep
ms.openlocfilehash: d8f9d84c5e9c0df4e9e985c10fe10f63a2f88214
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a><span data-ttu-id="2c1d0-103">在 Azure VM 上安裝 LEMP 網頁伺服器</span><span class="sxs-lookup"><span data-stu-id="2c1d0-103">Install a LEMP web server on an Azure VM</span></span>
<span data-ttu-id="2c1d0-104">本文將告訴您如何 toodeploy NGINX 網頁伺服器、 MySQL 和 Ubuntu VM 在 Azure 上的 PHP （hello LEMP 堆疊）。</span><span class="sxs-lookup"><span data-stu-id="2c1d0-104">This article walks you through how toodeploy an NGINX web server, MySQL, and PHP (hello LEMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="2c1d0-105">hello LEMP 堆疊是常用替代 toohello [LAMP 堆疊](tutorial-lamp-stack.md)，您也可以安裝在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="2c1d0-105">hello LEMP stack is an alternative toohello popular [LAMP stack](tutorial-lamp-stack.md), which you can also install in Azure.</span></span> <span data-ttu-id="2c1d0-106">toosee hello LEMP 伺服器在動作中，您可以選擇性地安裝和設定 WordPress 網站。</span><span class="sxs-lookup"><span data-stu-id="2c1d0-106">toosee hello LEMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="2c1d0-107">在本教學課程中，您了解如何：</span><span class="sxs-lookup"><span data-stu-id="2c1d0-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2c1d0-108">建立 Ubuntu VM (hello LEMP 堆疊中的 hello 'L')</span><span class="sxs-lookup"><span data-stu-id="2c1d0-108">Create an Ubuntu VM (hello 'L' in hello LEMP stack)</span></span>
> * <span data-ttu-id="2c1d0-109">針對 Web 流量開啟連接埠 80</span><span class="sxs-lookup"><span data-stu-id="2c1d0-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="2c1d0-110">安裝 NGINX、MySQL 和 PHP</span><span class="sxs-lookup"><span data-stu-id="2c1d0-110">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="2c1d0-111">驗證安裝和設定</span><span class="sxs-lookup"><span data-stu-id="2c1d0-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="2c1d0-112">Hello LEMP 伺服器上安裝 WordPress</span><span class="sxs-lookup"><span data-stu-id="2c1d0-112">Install WordPress on hello LEMP server</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2c1d0-113">如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="2c1d0-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="2c1d0-114">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="2c1d0-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="2c1d0-115">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="2c1d0-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a><span data-ttu-id="2c1d0-116">安裝 NGINX、MySQL 和 PHP</span><span class="sxs-lookup"><span data-stu-id="2c1d0-116">Install NGINX, MySQL, and PHP</span></span>

<span data-ttu-id="2c1d0-117">執行下列命令 tooupdate Ubuntu 封裝來源的 hello 和 NGINX、 MySQL 和 PHP 安裝。</span><span class="sxs-lookup"><span data-stu-id="2c1d0-117">Run hello following command tooupdate Ubuntu package sources and install NGINX, MySQL, and PHP.</span></span> 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

<span data-ttu-id="2c1d0-118">您會提示的 tooinstall hello 套件以及其他相依性。</span><span class="sxs-lookup"><span data-stu-id="2c1d0-118">You are prompted tooinstall hello packages and other dependencies.</span></span> <span data-ttu-id="2c1d0-119">出現提示時，設定根密碼 MySQL，然後 [Enter] toocontinue。</span><span class="sxs-lookup"><span data-stu-id="2c1d0-119">When prompted, set a root password for MySQL, and then [Enter] toocontinue.</span></span> <span data-ttu-id="2c1d0-120">請遵循其餘提示 hello。</span><span class="sxs-lookup"><span data-stu-id="2c1d0-120">Follow hello remaining prompts.</span></span> <span data-ttu-id="2c1d0-121">此程序會 hello 最小必要的 PHP 延伸模組需要 toouse PHP 安裝 MySQL。</span><span class="sxs-lookup"><span data-stu-id="2c1d0-121">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![MySQL 根密碼頁面][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="2c1d0-123">驗證安裝和設定</span><span class="sxs-lookup"><span data-stu-id="2c1d0-123">Verify installation and configuration</span></span>


### <a name="nginx"></a><span data-ttu-id="2c1d0-124">NGINX</span><span class="sxs-lookup"><span data-stu-id="2c1d0-124">NGINX</span></span>

<span data-ttu-id="2c1d0-125">請檢查 NGINX hello 版本以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="2c1d0-125">Check hello version of NGINX with hello following command:</span></span>
```bash
nginx -v
```

<span data-ttu-id="2c1d0-126">NGINX 安裝，且連接埠 80 開啟 tooyour VM、 hello web 伺服器現在可以從 hello 存取網際網路。</span><span class="sxs-lookup"><span data-stu-id="2c1d0-126">With NGINX installed, and port 80 open tooyour VM, hello web server can now be accessed from hello internet.</span></span> <span data-ttu-id="2c1d0-127">tooview hello NGINX  褖畫惎 頁面上，開啟網頁瀏覽器，並輸入 hello VM 的 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2c1d0-127">tooview hello NGINX welcome page, open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="2c1d0-128">使用 hello 用 tooSSH toohello VM 公用 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="2c1d0-128">Use hello public IP address you used tooSSH toohello VM:</span></span>

![NGINX 預設網頁][3]


### <a name="mysql"></a><span data-ttu-id="2c1d0-130">MySQL</span><span class="sxs-lookup"><span data-stu-id="2c1d0-130">MySQL</span></span>

<span data-ttu-id="2c1d0-131">以下列命令的 hello 檢查 hello MySQL 版本 (請注意 hello 資本`V`參數):</span><span class="sxs-lookup"><span data-stu-id="2c1d0-131">Check hello version of MySQL with hello following command (note hello capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="2c1d0-132">我們建議您執行下列指令碼 toohelp 安全 hello 安裝 MySQL hello:</span><span class="sxs-lookup"><span data-stu-id="2c1d0-132">We recommend running hello following script toohelp secure hello installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="2c1d0-133">輸入 MySQL 根密碼，並設定您的環境的 hello 安全性設定。</span><span class="sxs-lookup"><span data-stu-id="2c1d0-133">Enter your MySQL root password, and configure hello security settings for your environment.</span></span>

<span data-ttu-id="2c1d0-134">如果您想 toocreate MySQL 資料庫，新增使用者，或變更組態設定，登入 tooMySQL:</span><span class="sxs-lookup"><span data-stu-id="2c1d0-134">If you want toocreate a MySQL database, add users, or change configuration settings, login tooMySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="2c1d0-135">當完成時，結束 hello mysql 提示字元中輸入`\q`。</span><span class="sxs-lookup"><span data-stu-id="2c1d0-135">When done, exit hello mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="2c1d0-136">PHP</span><span class="sxs-lookup"><span data-stu-id="2c1d0-136">PHP</span></span>

<span data-ttu-id="2c1d0-137">核取 hello 版本的 PHP 以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="2c1d0-137">Check hello version of PHP with hello following command:</span></span>

```bash
php -v
```

<span data-ttu-id="2c1d0-138">設定 NGINX toouse hello PHP 的 FastCGI 處理序管理員 (PHP FPM)。</span><span class="sxs-lookup"><span data-stu-id="2c1d0-138">Configure NGINX toouse hello PHP FastCGI Process Manager (PHP-FPM).</span></span> <span data-ttu-id="2c1d0-139">執行下列命令 tooback hello 原始 NGINX 伺服器封鎖組態檔，然後編輯在您選擇的編輯器中的 hello 原始檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="2c1d0-139">Run hello following commands tooback up hello original NGINX server block config file and then edit hello original file in an editor of your choice:</span></span>

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

<span data-ttu-id="2c1d0-140">在 hello 編輯器取代 hello 內容`/etc/nginx/sites-available/default`hello 下列。</span><span class="sxs-lookup"><span data-stu-id="2c1d0-140">In hello editor, replace hello contents of `/etc/nginx/sites-available/default` with hello following.</span></span> <span data-ttu-id="2c1d0-141">如需說明 hello 設定 hello 註解，請參閱。</span><span class="sxs-lookup"><span data-stu-id="2c1d0-141">See hello comments for explanation of hello settings.</span></span> <span data-ttu-id="2c1d0-142">取代為您 VM 的 hello 公用 IP 位址*yourPublicIPAddress*，並保留 hello 其餘設定。</span><span class="sxs-lookup"><span data-stu-id="2c1d0-142">Substitute hello public IP address of your VM for *yourPublicIPAddress*, and leave hello remaining settings.</span></span> <span data-ttu-id="2c1d0-143">然後儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="2c1d0-143">Then save hello file.</span></span>

```
server {
    listen 80 default_server;
    listen [::]:80 default_server;

    root /var/www/html;
    # Homepage of website is index.php
    index index.php;

    server_name yourPublicIPAddress;

    location / {
        try_files $uri $uri/ =404;
    }

    # Include FastCGI configuration for NGINX
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.0-fpm.sock;
    }
}
```

<span data-ttu-id="2c1d0-144">請檢查語法錯誤的 hello NGINX 組態：</span><span class="sxs-lookup"><span data-stu-id="2c1d0-144">Check hello NGINX configuration for syntax errors:</span></span>

```bash
sudo nginx -t
```

<span data-ttu-id="2c1d0-145">如果 hello 語法正確，請重新啟動 NGINX hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="2c1d0-145">If hello syntax is correct, restart NGINX with hello following command:</span></span>

```bash
sudo service nginx restart
```

<span data-ttu-id="2c1d0-146">如果您想進一步 tootest，建立快速的 PHP 資訊頁面 tooview 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="2c1d0-146">If you want tootest further, create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="2c1d0-147">hello，下列命令會建立 hello PHP 資訊頁面：</span><span class="sxs-lookup"><span data-stu-id="2c1d0-147">hello following command creates hello PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



<span data-ttu-id="2c1d0-148">現在您可以檢查您所建立的 hello PHP 資訊頁面。</span><span class="sxs-lookup"><span data-stu-id="2c1d0-148">Now you can check hello PHP info page you created.</span></span> <span data-ttu-id="2c1d0-149">開啟瀏覽器並移過`http://yourPublicIPAddress/info.php`。</span><span class="sxs-lookup"><span data-stu-id="2c1d0-149">Open a browser and go too`http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="2c1d0-150">取代您的 VM hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2c1d0-150">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="2c1d0-151">它看起來應該類似 toothis 映像。</span><span class="sxs-lookup"><span data-stu-id="2c1d0-151">It should look similar toothis image.</span></span>

![PHP 資訊網頁][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a><span data-ttu-id="2c1d0-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2c1d0-153">Next steps</span></span>

<span data-ttu-id="2c1d0-154">在本教學課程中，您已在 Azure 中部署 LEMP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="2c1d0-154">In this tutorial, you deployed a LEMP server in Azure.</span></span> <span data-ttu-id="2c1d0-155">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="2c1d0-155">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2c1d0-156">建立 Ubuntu VM</span><span class="sxs-lookup"><span data-stu-id="2c1d0-156">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="2c1d0-157">針對 Web 流量開啟連接埠 80</span><span class="sxs-lookup"><span data-stu-id="2c1d0-157">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="2c1d0-158">安裝 NGINX、MySQL 和 PHP</span><span class="sxs-lookup"><span data-stu-id="2c1d0-158">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="2c1d0-159">驗證安裝和設定</span><span class="sxs-lookup"><span data-stu-id="2c1d0-159">Verify installation and configuration</span></span>
> * <span data-ttu-id="2c1d0-160">安裝 WordPress hello LEMP 堆疊上</span><span class="sxs-lookup"><span data-stu-id="2c1d0-160">Install WordPress on hello LEMP stack</span></span>

<span data-ttu-id="2c1d0-161">如何前進 toohello 下一個教學課程 toolearn toosecure 網頁伺服器使用 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="2c1d0-161">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2c1d0-162">使用 SSL 保護網路伺服器</span><span class="sxs-lookup"><span data-stu-id="2c1d0-162">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
