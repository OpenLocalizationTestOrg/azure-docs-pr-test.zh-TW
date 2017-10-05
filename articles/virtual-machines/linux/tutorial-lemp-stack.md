---
title: "在 Azure 的 Linux 虛擬機器上部署 LEMP | Microsoft Docs"
description: "教學課程 - 在 Azure 中的 Linux VM 上安裝 LEMP 堆疊"
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
ms.openlocfilehash: 653af144eb12cacf955f96a5442efd73add38e88
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a><span data-ttu-id="27e69-103">在 Azure VM 上安裝 LEMP 網頁伺服器</span><span class="sxs-lookup"><span data-stu-id="27e69-103">Install a LEMP web server on an Azure VM</span></span>
<span data-ttu-id="27e69-104">本文會逐步引導您在 Azure 中的 Ubuntu VM 上部署 NGINX 網頁伺服器、MySQL 和 PHP (LEMP 堆疊)。</span><span class="sxs-lookup"><span data-stu-id="27e69-104">This article walks you through how to deploy an NGINX web server, MySQL, and PHP (the LEMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="27e69-105">LEMP 堆疊可替代熱門的 [LAMP 堆疊](tutorial-lamp-stack.md) (後者也可以安裝在 Azure 中)。</span><span class="sxs-lookup"><span data-stu-id="27e69-105">The LEMP stack is an alternative to the popular [LAMP stack](tutorial-lamp-stack.md), which you can also install in Azure.</span></span> <span data-ttu-id="27e69-106">若要查看作用中的 LEMP 伺服器，您可以選擇安裝及設定 WordPress 網站。</span><span class="sxs-lookup"><span data-stu-id="27e69-106">To see the LEMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="27e69-107">在本教學課程中，您了解如何：</span><span class="sxs-lookup"><span data-stu-id="27e69-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="27e69-108">建立 Ubuntu VM (LEMP 堆疊中的 'L')</span><span class="sxs-lookup"><span data-stu-id="27e69-108">Create an Ubuntu VM (the 'L' in the LEMP stack)</span></span>
> * <span data-ttu-id="27e69-109">針對 Web 流量開啟連接埠 80</span><span class="sxs-lookup"><span data-stu-id="27e69-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="27e69-110">安裝 NGINX、MySQL 和 PHP</span><span class="sxs-lookup"><span data-stu-id="27e69-110">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="27e69-111">驗證安裝和設定</span><span class="sxs-lookup"><span data-stu-id="27e69-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="27e69-112">在 LEMP 伺服器上安裝 WordPress</span><span class="sxs-lookup"><span data-stu-id="27e69-112">Install WordPress on the LEMP server</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="27e69-113">如果您選擇在本機安裝和使用 CLI，本教學課程會要求您執行 Azure CLI 2.0.4 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="27e69-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="27e69-114">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="27e69-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="27e69-115">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="27e69-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a><span data-ttu-id="27e69-116">安裝 NGINX、MySQL 和 PHP</span><span class="sxs-lookup"><span data-stu-id="27e69-116">Install NGINX, MySQL, and PHP</span></span>

<span data-ttu-id="27e69-117">執行下列命令以更新 Ubuntu 套件來源，並安裝 NGINX、MySQL 和 PHP。</span><span class="sxs-lookup"><span data-stu-id="27e69-117">Run the following command to update Ubuntu package sources and install NGINX, MySQL, and PHP.</span></span> 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

<span data-ttu-id="27e69-118">系統會提示您安裝套件和其他相依性。</span><span class="sxs-lookup"><span data-stu-id="27e69-118">You are prompted to install the packages and other dependencies.</span></span> <span data-ttu-id="27e69-119">出現提示時，請為 MySQL 設定根密碼，然後按 [Enter] 以繼續。</span><span class="sxs-lookup"><span data-stu-id="27e69-119">When prompted, set a root password for MySQL, and then [Enter] to continue.</span></span> <span data-ttu-id="27e69-120">按照其餘的提示來進行。</span><span class="sxs-lookup"><span data-stu-id="27e69-120">Follow the remaining prompts.</span></span> <span data-ttu-id="27e69-121">此程序會安裝使用 PHP 搭配 MySQL 時所需的基本必要 PHP 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="27e69-121">This process installs the minimum required PHP extensions needed to use PHP with MySQL.</span></span> 

![MySQL 根密碼頁面][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="27e69-123">驗證安裝和設定</span><span class="sxs-lookup"><span data-stu-id="27e69-123">Verify installation and configuration</span></span>


### <a name="nginx"></a><span data-ttu-id="27e69-124">NGINX</span><span class="sxs-lookup"><span data-stu-id="27e69-124">NGINX</span></span>

<span data-ttu-id="27e69-125">使用下列命令檢查 NGINX 的版本：</span><span class="sxs-lookup"><span data-stu-id="27e69-125">Check the version of NGINX with the following command:</span></span>
```bash
nginx -v
```

<span data-ttu-id="27e69-126">安裝 NGINX 後，且連接埠 80 對您的 VM 開啟，即可立即從網際網路存取網頁伺服器。</span><span class="sxs-lookup"><span data-stu-id="27e69-126">With NGINX installed, and port 80 open to your VM, the web server can now be accessed from the internet.</span></span> <span data-ttu-id="27e69-127">若要檢視 NGINX 歡迎頁面，請開啟網頁瀏覽器，並輸入 VM 的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="27e69-127">To view the NGINX welcome page, open a web browser, and enter the public IP address of the VM.</span></span> <span data-ttu-id="27e69-128">使用您在透過 SSH 連線到 VM 時所使用的公用 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="27e69-128">Use the public IP address you used to SSH to the VM:</span></span>

![NGINX 預設網頁][3]


### <a name="mysql"></a><span data-ttu-id="27e69-130">MySQL</span><span class="sxs-lookup"><span data-stu-id="27e69-130">MySQL</span></span>

<span data-ttu-id="27e69-131">使用下列命令檢查 MySQL 的版本 (請注意 `V` 參數是大寫)：</span><span class="sxs-lookup"><span data-stu-id="27e69-131">Check the version of MySQL with the following command (note the capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="27e69-132">我們建議您執行下列指令碼來協助保護 MySQL 的安裝：</span><span class="sxs-lookup"><span data-stu-id="27e69-132">We recommend running the following script to help secure the installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="27e69-133">輸入 MySQL 根密碼，並為您的環境設定安全性設定。</span><span class="sxs-lookup"><span data-stu-id="27e69-133">Enter your MySQL root password, and configure the security settings for your environment.</span></span>

<span data-ttu-id="27e69-134">如果您想要建立 MySQL 資料庫，請新增使用者或變更組態設定，登入 MySQL：</span><span class="sxs-lookup"><span data-stu-id="27e69-134">If you want to create a MySQL database, add users, or change configuration settings, login to MySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="27e69-135">完成後，輸入 `\q` 以結束 mysql 提示字元。</span><span class="sxs-lookup"><span data-stu-id="27e69-135">When done, exit the mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="27e69-136">PHP</span><span class="sxs-lookup"><span data-stu-id="27e69-136">PHP</span></span>

<span data-ttu-id="27e69-137">使用下列命令檢查 PHP 的版本：</span><span class="sxs-lookup"><span data-stu-id="27e69-137">Check the version of PHP with the following command:</span></span>

```bash
php -v
```

<span data-ttu-id="27e69-138">將 NGINX 設定為使用 PHP FastCGI Process Manager (PHP-FPM)。</span><span class="sxs-lookup"><span data-stu-id="27e69-138">Configure NGINX to use the PHP FastCGI Process Manager (PHP-FPM).</span></span> <span data-ttu-id="27e69-139">執行下列命令來備份原始的 NGINX 伺服器區塊組態檔，然後使用您選擇的編輯器編輯原始檔案：</span><span class="sxs-lookup"><span data-stu-id="27e69-139">Run the following commands to back up the original NGINX server block config file and then edit the original file in an editor of your choice:</span></span>

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

<span data-ttu-id="27e69-140">在編輯器中，將 `/etc/nginx/sites-available/default` 的內容取代為下列項目。</span><span class="sxs-lookup"><span data-stu-id="27e69-140">In the editor, replace the contents of `/etc/nginx/sites-available/default` with the following.</span></span> <span data-ttu-id="27e69-141">如需設定的說明，請參閱註解。</span><span class="sxs-lookup"><span data-stu-id="27e69-141">See the comments for explanation of the settings.</span></span> <span data-ttu-id="27e69-142">以您 VM 的公用 IP 位址來替代 *yourPublicIPAddress*，其餘設定則予以保留。</span><span class="sxs-lookup"><span data-stu-id="27e69-142">Substitute the public IP address of your VM for *yourPublicIPAddress*, and leave the remaining settings.</span></span> <span data-ttu-id="27e69-143">然後儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="27e69-143">Then save the file.</span></span>

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

<span data-ttu-id="27e69-144">檢查 NGINX 組態中是否有語法錯誤：</span><span class="sxs-lookup"><span data-stu-id="27e69-144">Check the NGINX configuration for syntax errors:</span></span>

```bash
sudo nginx -t
```

<span data-ttu-id="27e69-145">如果語法正確，請使用下列命令重新啟動 NGINX：</span><span class="sxs-lookup"><span data-stu-id="27e69-145">If the syntax is correct, restart NGINX with the following command:</span></span>

```bash
sudo service nginx restart
```

<span data-ttu-id="27e69-146">如果您想要進一步測試，請建立要在瀏覽器中檢視的快速 PHP 資訊網頁。</span><span class="sxs-lookup"><span data-stu-id="27e69-146">If you want to test further, create a quick PHP info page to view in a browser.</span></span> <span data-ttu-id="27e69-147">下列命令會建立 PHP 資訊網頁：</span><span class="sxs-lookup"><span data-stu-id="27e69-147">The following command creates the PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



<span data-ttu-id="27e69-148">現在您可以檢查您所建立的 PHP 資訊網頁。</span><span class="sxs-lookup"><span data-stu-id="27e69-148">Now you can check the PHP info page you created.</span></span> <span data-ttu-id="27e69-149">開啟瀏覽器並前往 `http://yourPublicIPAddress/info.php`。</span><span class="sxs-lookup"><span data-stu-id="27e69-149">Open a browser and go to `http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="27e69-150">替換為您 VM 的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="27e69-150">Substitute the public IP address of your VM.</span></span> <span data-ttu-id="27e69-151">該頁面看起來應該類似下圖。</span><span class="sxs-lookup"><span data-stu-id="27e69-151">It should look similar to this image.</span></span>

![PHP 資訊網頁][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a><span data-ttu-id="27e69-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="27e69-153">Next steps</span></span>

<span data-ttu-id="27e69-154">在本教學課程中，您已在 Azure 中部署 LEMP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="27e69-154">In this tutorial, you deployed a LEMP server in Azure.</span></span> <span data-ttu-id="27e69-155">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="27e69-155">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="27e69-156">建立 Ubuntu VM</span><span class="sxs-lookup"><span data-stu-id="27e69-156">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="27e69-157">針對 Web 流量開啟連接埠 80</span><span class="sxs-lookup"><span data-stu-id="27e69-157">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="27e69-158">安裝 NGINX、MySQL 和 PHP</span><span class="sxs-lookup"><span data-stu-id="27e69-158">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="27e69-159">驗證安裝和設定</span><span class="sxs-lookup"><span data-stu-id="27e69-159">Verify installation and configuration</span></span>
> * <span data-ttu-id="27e69-160">在 LEMP 堆疊上安裝 WordPress</span><span class="sxs-lookup"><span data-stu-id="27e69-160">Install WordPress on the LEMP stack</span></span>

<span data-ttu-id="27e69-161">前進到下一個教學課程，以了解如何使用 SSL 憑證保護 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="27e69-161">Advance to the next tutorial to learn how to secure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="27e69-162">使用 SSL 保護網路伺服器</span><span class="sxs-lookup"><span data-stu-id="27e69-162">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
