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
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a>在 Azure VM 上安裝 LEMP 網頁伺服器
本文將告訴您如何 toodeploy NGINX 網頁伺服器、 MySQL 和 Ubuntu VM 在 Azure 上的 PHP （hello LEMP 堆疊）。 hello LEMP 堆疊是常用替代 toohello [LAMP 堆疊](tutorial-lamp-stack.md)，您也可以安裝在 Azure 中。 toosee hello LEMP 伺服器在動作中，您可以選擇性地安裝和設定 WordPress 網站。 在本教學課程中，您了解如何：

> [!div class="checklist"]
> * 建立 Ubuntu VM (hello LEMP 堆疊中的 hello 'L')
> * 針對 Web 流量開啟連接埠 80
> * 安裝 NGINX、MySQL 和 PHP
> * 驗證安裝和設定
> * Hello LEMP 伺服器上安裝 WordPress


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a>安裝 NGINX、MySQL 和 PHP

執行下列命令 tooupdate Ubuntu 封裝來源的 hello 和 NGINX、 MySQL 和 PHP 安裝。 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

您會提示的 tooinstall hello 套件以及其他相依性。 出現提示時，設定根密碼 MySQL，然後 [Enter] toocontinue。 請遵循其餘提示 hello。 此程序會 hello 最小必要的 PHP 延伸模組需要 toouse PHP 安裝 MySQL。 

![MySQL 根密碼頁面][1]

## <a name="verify-installation-and-configuration"></a>驗證安裝和設定


### <a name="nginx"></a>NGINX

請檢查 NGINX hello 版本以 hello 下列命令：
```bash
nginx -v
```

NGINX 安裝，且連接埠 80 開啟 tooyour VM、 hello web 伺服器現在可以從 hello 存取網際網路。 tooview hello NGINX  褖畫惎 頁面上，開啟網頁瀏覽器，並輸入 hello VM 的 hello 公用 IP 位址。 使用 hello 用 tooSSH toohello VM 公用 IP 位址：

![NGINX 預設網頁][3]


### <a name="mysql"></a>MySQL

以下列命令的 hello 檢查 hello MySQL 版本 (請注意 hello 資本`V`參數):

```bash
msql -V
```

我們建議您執行下列指令碼 toohelp 安全 hello 安裝 MySQL hello:

```bash
mysql_secure_installation
```

輸入 MySQL 根密碼，並設定您的環境的 hello 安全性設定。

如果您想 toocreate MySQL 資料庫，新增使用者，或變更組態設定，登入 tooMySQL:

```bash
mysql -u root -p
```

當完成時，結束 hello mysql 提示字元中輸入`\q`。

### <a name="php"></a>PHP

核取 hello 版本的 PHP 以 hello 下列命令：

```bash
php -v
```

設定 NGINX toouse hello PHP 的 FastCGI 處理序管理員 (PHP FPM)。 執行下列命令 tooback hello 原始 NGINX 伺服器封鎖組態檔，然後編輯在您選擇的編輯器中的 hello 原始檔案的 hello:

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

在 hello 編輯器取代 hello 內容`/etc/nginx/sites-available/default`hello 下列。 如需說明 hello 設定 hello 註解，請參閱。 取代為您 VM 的 hello 公用 IP 位址*yourPublicIPAddress*，並保留 hello 其餘設定。 然後儲存 hello 檔案。

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

請檢查語法錯誤的 hello NGINX 組態：

```bash
sudo nginx -t
```

如果 hello 語法正確，請重新啟動 NGINX hello 下列命令：

```bash
sudo service nginx restart
```

如果您想進一步 tootest，建立快速的 PHP 資訊頁面 tooview 瀏覽器中。 hello，下列命令會建立 hello PHP 資訊頁面：

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



現在您可以檢查您所建立的 hello PHP 資訊頁面。 開啟瀏覽器並移過`http://yourPublicIPAddress/info.php`。 取代您的 VM hello 公用 IP 位址。 它看起來應該類似 toothis 映像。

![PHP 資訊網頁][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已在 Azure 中部署 LEMP 伺服器。 您已了解如何︰

> [!div class="checklist"]
> * 建立 Ubuntu VM
> * 針對 Web 流量開啟連接埠 80
> * 安裝 NGINX、MySQL 和 PHP
> * 驗證安裝和設定
> * 安裝 WordPress hello LEMP 堆疊上

如何前進 toohello 下一個教學課程 toolearn toosecure 網頁伺服器使用 SSL 憑證。

> [!div class="nextstepaction"]
> [使用 SSL 保護網路伺服器](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
