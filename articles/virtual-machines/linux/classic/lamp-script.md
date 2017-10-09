---
title: "aaaUse hello CustomScript 延伸模組，Linux VM 上 |Microsoft 文件"
description: "了解 toouse hello CustomScript 延伸模組 toodeploy 應用程式在 Azure 中 Linux 虛擬機器建立使用 hello 傳統部署模型的方式。"
editor: tysonn
manager: timlt
documentationcenter: 
services: virtual-machines-linux
author: gbowerman
tags: azure-service-management
ms.assetid: e535241d-feca-4412-b07a-67c936ba88a0
ms.service: virtual-machines-linux
ms.workload: multiple
ms.tgt_pltfrm: linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: guybo
ms.openlocfilehash: 864a586e70093eefbabc065a3c05e1cf9e315704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-lamp-app-using-hello-azure-customscript-extension-for-linux"></a>部署使用適用於 Linux 的 hello Azure CustomScript 延伸模組的燈應用程式
> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 如需部署使用 hello 資源管理員模型 LAMP 堆疊的相關資訊，請參閱[這裡](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

hello 適用於 Linux 的 Microsoft Azure CustomScript 延伸模組提供方式 toocustomize 您虛擬機器 (Vm) 執行任意 hello VM （例如，Python 和 Bash） 所支援的任何指令碼語言撰寫的程式碼。 這可提供非常彈性的方式 tooautomate 應用程式部署 toomultiple 電腦。

您可以部署 hello CustomScript 延伸模組使用 hello Azure 入口網站、 Windows PowerShell 或 hello Azure 命令列介面 (Azure CLI)。

在本文中，我們會使用 hello Azure CLI toodeploy 簡單燈應用程式 tooan Ubuntu VM 使用建立 hello 傳統部署模型。

## <a name="prerequisites"></a>必要條件
在此範例中，會先建立兩個執行 Ubuntu 14.04 或更新版本的 Azure VM。 hello Vm 稱為*指令碼 vm*和*燈 vm*。 當您建立 hello Vm 時，請使用唯一名稱。 一個是使用的 toorun hello CLI 命令，其中一個是使用的 toodeploy hello 燈應用程式。

您也需要 Azure 儲存體帳戶和金鑰 tooaccess it （可取得這個從 hello Azure 入口網站）。

如果您需要在 Azure 上建立 Linux Vm 的說明，請參閱太[建立執行 Linux 之虛擬機器](createportal.md)。

hello 安裝命令假設 Ubuntu，不過您可以調整 hello 安裝的任何支援的 Linux distro。

hello 指令碼 vm VM 需要安裝 Azure CLI，與工作連接 tooAzure toohave。 說明，請參閱太[安裝及設定 hello Azure 命令列介面](../../../cli-install-nodejs.md)。

## <a name="upload-a-script"></a>上傳指令碼
我們將使用遠端的 VM tooinstall hello LAMP 堆疊上的 hello CustomScript 延伸模組 toorun 指令碼，並建立 PHP 網頁。 從任何地方順序 tooaccess hello 指令碼中我們會將它當做 Azure blob 上傳。

### <a name="script-overview"></a>指令碼概觀
hello 指令碼範例會安裝 （包括設定無訊息安裝的 MySQL） LAMP 堆疊 tooUbuntu、 將簡單的 PHP 檔案，並啟動 Apache。

    #!/bin/bash
    # set up a silent install of MySQL
    dbpass="mySQLPassw0rd"

    export DEBIAN_FRONTEND=noninteractive
    echo mysql-server-5.6 mysql-server/root_password password $dbpass | debconf-set-selections
    echo mysql-server-5.6 mysql-server/root_password_again password $dbpass | debconf-set-selections

    # install hello LAMP stack
    apt-get -y install apache2 mysql-server php5 php5-mysql  

    # write some PHP
    echo \<center\>\<h1\>My Demo App\</h1\>\<br/\>\</center\> > /var/www/html/phpinfo.php
    echo \<\?php phpinfo\(\)\; \?\> >> /var/www/html/phpinfo.php

    # restart Apache
    apachectl restart

### <a name="upload-script"></a>上傳指令碼
將 hello 指令碼儲存為文字檔案，例如*install_lamp.sh*，然後再上載 tooAzure 儲存體。 您可以使用 Azure CLI，輕鬆執行這個動作。 hello 下列範例會上傳 hello 檔案 tooa 儲存體容器名稱為 「 指令碼 」。 如果 hello 容器不存在，您將需要 toocreate 它第一次。

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

也會建立描述 toodownload hello 從 Azure 儲存體的指令碼的方式在 JSON 檔案。 儲存為*public_config.json* （取代"mystorage"hello 您的儲存體帳戶名稱）：

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-hello-extension"></a>Hello 延伸模組部署
現在您可以使用 hello 下一個命令 toodeploy hello Linux CustomScript 延伸模組 toohello 遠端 VM 使用 hello Azure CLI。

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

hello 前一個命令會下載並執行 hello *install_lamp.sh*指令碼的 VM 稱為的 hello*燈 vm*。

因為 hello 應用程式包含 web 伺服器，請記住 tooopen HTTP 接聽連接埠上 hello 遠端 VM 與 hello 下一個命令。

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a>監視與疑難排解
您可以檢查 hello 自訂的指令碼會藉由查看 hello 記錄檔上 hello 遠端 VM 的程度。 SSH 太*燈 vm*和結尾 hello 記錄檔與 hello 下一個命令。

    cd /var/log/azure/customscript
    tail -f handler.log

執行 hello CustomScript 延伸模組之後，您可以瀏覽 toohello PHP 頁面，您建立的資訊。 hello PHP 頁面上的這篇文章中的 hello 範例*http://lamp-vm.cloudapp.net/phpinfo.php*。

## <a name="additional-resources"></a>其他資源
您可以使用 hello 相同的基本步驟 toodeploy 更複雜的應用程式。 在此範例中 hello 安裝指令碼已儲存為 Azure 儲存體中的公用 blob。 較安全的選項會是 toostore hello 安裝指令碼為安全的 blob 與[安全的存取簽章](https://msdn.microsoft.com/library/azure/ee395415.aspx)(SAS)。

適用於 Azure CLI、 Linux 和 hello CustomScript 延伸模組的其他資源會列在下一個。

[使用 CustomScript 延伸模組以將 Linux VM 自訂工作自動化](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[Azure Linux 延伸模組 (GitHub)](https://github.com/Azure/azure-linux-extensions)