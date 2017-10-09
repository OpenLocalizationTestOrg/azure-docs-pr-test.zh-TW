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
# <a name="install-a-lamp-web-server-on-an-azure-vm"></a>在 Azure VM 上安裝 LAMP 網頁伺服器
本文將告訴您如何 toodeploy Apache web 伺服器、 MySQL 和 Ubuntu VM 在 Azure 上的 PHP （hello LAMP 堆疊）。 如果您偏好 hello NGINX 網頁伺服器，請參閱 hello [LEMP 堆疊](tutorial-lemp-stack.md)教學課程。 toosee hello 燈伺服器在動作中，您可以選擇性地安裝和設定 WordPress 網站。 在本教學課程中，您了解如何：

> [!div class="checklist"]
> * 建立 Ubuntu VM (hello LAMP 堆疊中的 hello 'L')
> * 針對 Web 流量開啟連接埠 80
> * 安裝 Apache、MySQL 和 PHP
> * 驗證安裝和設定
> * Hello 燈伺服器上安裝 WordPress


如需 hello LAMP 堆疊，包括建議的生產環境，請參閱 hello [Ubuntu 文件](https://help.ubuntu.com/community/ApacheMySQLPHP)。

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-apache-mysql-and-php"></a>安裝 Apache、MySQL 和 PHP

執行下列命令 tooupdate Ubuntu 封裝來源的 hello 並安裝 Apache、 MySQL 和 PHP。 請注意結尾 hello hello 命令 hello 插入號 (^)。


```bash
sudo apt update && sudo apt install lamp-server^
```



您會提示的 tooinstall hello 套件以及其他相依性。 出現提示時，設定根密碼 MySQL，然後 [Enter] toocontinue。 請遵循其餘提示 hello。 此程序會 hello 最小必要的 PHP 延伸模組需要 toouse PHP 安裝 MySQL。 

![MySQL 根密碼頁面][1]

## <a name="verify-installation-and-configuration"></a>驗證安裝和設定


### <a name="apache"></a>Apache

核取 hello 版本的 Apache 以 hello 下列命令：
```bash
apache2 -v
```

Apache 安裝，且連接埠 80 開啟 tooyour VM、 hello web 伺服器現在可以從 hello 存取網際網路。 tooview hello Apache2 Ubuntu 預設頁面上，開啟網頁瀏覽器，並輸入 hello VM 的 hello 公用 IP 位址。 使用 hello 用 tooSSH toohello VM 公用 IP 位址：

![Apache 預設網頁][3]


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

如果您想進一步 tootest，建立快速的 PHP 資訊頁面 tooview 瀏覽器中。 hello，下列命令會建立 hello PHP 資訊頁面：

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```

現在您可以檢查您所建立的 hello PHP 資訊頁面。 開啟瀏覽器並移過`http://yourPublicIPAddress/info.php`。 取代您的 VM hello 公用 IP 位址。 它看起來應該類似 toothis 映像。

![PHP 資訊網頁][2]

[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]


## <a name="next-steps"></a>後續步驟

在本教學課程中，您已在 Azure 中部署 LAMP 伺服器。 您已了解如何︰

> [!div class="checklist"]
> * 建立 Ubuntu VM
> * 針對 Web 流量開啟連接埠 80
> * 安裝 Apache、MySQL 和 PHP
> * 驗證安裝和設定
> * Hello 燈伺服器上安裝 WordPress

如何前進 toohello 下一個教學課程 toolearn toosecure 網頁伺服器使用 SSL 憑證。

> [!div class="nextstepaction"]
> [使用 SSL 保護網路伺服器](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lamp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lamp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lamp-stack/apachesuccesspage.png