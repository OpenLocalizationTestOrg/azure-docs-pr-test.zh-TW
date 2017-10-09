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
# <a name="deploy-a-lamp-app-using-hello-azure-customscript-extension-for-linux"></a><span data-ttu-id="5ae35-103">部署使用適用於 Linux 的 hello Azure CustomScript 延伸模組的燈應用程式</span><span class="sxs-lookup"><span data-stu-id="5ae35-103">Deploy a LAMP app using hello Azure CustomScript Extension for Linux</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="5ae35-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="5ae35-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="5ae35-105">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="5ae35-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="5ae35-106">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="5ae35-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="5ae35-107">如需部署使用 hello 資源管理員模型 LAMP 堆疊的相關資訊，請參閱[這裡](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="5ae35-107">For information about deploying a LAMP stack using hello Resource Manager model, see [here](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="5ae35-108">hello 適用於 Linux 的 Microsoft Azure CustomScript 延伸模組提供方式 toocustomize 您虛擬機器 (Vm) 執行任意 hello VM （例如，Python 和 Bash） 所支援的任何指令碼語言撰寫的程式碼。</span><span class="sxs-lookup"><span data-stu-id="5ae35-108">hello Microsoft Azure CustomScript Extension for Linux provides a way toocustomize your virtual machines (VMs) by running arbitrary code written in any scripting language supported by hello VM (for example, Python, and Bash).</span></span> <span data-ttu-id="5ae35-109">這可提供非常彈性的方式 tooautomate 應用程式部署 toomultiple 電腦。</span><span class="sxs-lookup"><span data-stu-id="5ae35-109">This provides a very flexible way tooautomate application deployment toomultiple machines.</span></span>

<span data-ttu-id="5ae35-110">您可以部署 hello CustomScript 延伸模組使用 hello Azure 入口網站、 Windows PowerShell 或 hello Azure 命令列介面 (Azure CLI)。</span><span class="sxs-lookup"><span data-stu-id="5ae35-110">You can deploy hello CustomScript Extension using hello Azure portal, Windows PowerShell, or hello Azure Command-Line Interface (Azure CLI).</span></span>

<span data-ttu-id="5ae35-111">在本文中，我們會使用 hello Azure CLI toodeploy 簡單燈應用程式 tooan Ubuntu VM 使用建立 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="5ae35-111">In this article we'll use hello Azure CLI toodeploy a simple LAMP application tooan Ubuntu VM created using hello classic deployment model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ae35-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="5ae35-112">Prerequisites</span></span>
<span data-ttu-id="5ae35-113">在此範例中，會先建立兩個執行 Ubuntu 14.04 或更新版本的 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="5ae35-113">For this example, first create two Azure VMs running Ubuntu 14.04 or later.</span></span> <span data-ttu-id="5ae35-114">hello Vm 稱為*指令碼 vm*和*燈 vm*。</span><span class="sxs-lookup"><span data-stu-id="5ae35-114">hello VMs are called *script-vm* and *lamp-vm*.</span></span> <span data-ttu-id="5ae35-115">當您建立 hello Vm 時，請使用唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="5ae35-115">Use unique names when you create hello VMs.</span></span> <span data-ttu-id="5ae35-116">一個是使用的 toorun hello CLI 命令，其中一個是使用的 toodeploy hello 燈應用程式。</span><span class="sxs-lookup"><span data-stu-id="5ae35-116">One is used toorun hello CLI commands and one is used toodeploy hello LAMP app.</span></span>

<span data-ttu-id="5ae35-117">您也需要 Azure 儲存體帳戶和金鑰 tooaccess it （可取得這個從 hello Azure 入口網站）。</span><span class="sxs-lookup"><span data-stu-id="5ae35-117">You also need an Azure Storage account and a key tooaccess it (you can get this from hello Azure portal).</span></span>

<span data-ttu-id="5ae35-118">如果您需要在 Azure 上建立 Linux Vm 的說明，請參閱太[建立執行 Linux 之虛擬機器](createportal.md)。</span><span class="sxs-lookup"><span data-stu-id="5ae35-118">If you need help creating Linux VMs on Azure refer too[Create a Virtual Machine Running Linux](createportal.md).</span></span>

<span data-ttu-id="5ae35-119">hello 安裝命令假設 Ubuntu，不過您可以調整 hello 安裝的任何支援的 Linux distro。</span><span class="sxs-lookup"><span data-stu-id="5ae35-119">hello install commands assume Ubuntu, but you can adapt hello installation for any supported Linux distro.</span></span>

<span data-ttu-id="5ae35-120">hello 指令碼 vm VM 需要安裝 Azure CLI，與工作連接 tooAzure toohave。</span><span class="sxs-lookup"><span data-stu-id="5ae35-120">hello script-vm VM needs toohave Azure CLI installed, with a working connection tooAzure.</span></span> <span data-ttu-id="5ae35-121">說明，請參閱太[安裝及設定 hello Azure 命令列介面](../../../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="5ae35-121">For help with this refer too[Install and Configure hello Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span>

## <a name="upload-a-script"></a><span data-ttu-id="5ae35-122">上傳指令碼</span><span class="sxs-lookup"><span data-stu-id="5ae35-122">Upload a script</span></span>
<span data-ttu-id="5ae35-123">我們將使用遠端的 VM tooinstall hello LAMP 堆疊上的 hello CustomScript 延伸模組 toorun 指令碼，並建立 PHP 網頁。</span><span class="sxs-lookup"><span data-stu-id="5ae35-123">We'll use hello CustomScript Extension toorun a script on a remote VM tooinstall hello LAMP stack and create a PHP page.</span></span> <span data-ttu-id="5ae35-124">從任何地方順序 tooaccess hello 指令碼中我們會將它當做 Azure blob 上傳。</span><span class="sxs-lookup"><span data-stu-id="5ae35-124">In order tooaccess hello script from anywhere we'll upload it as an Azure blob.</span></span>

### <a name="script-overview"></a><span data-ttu-id="5ae35-125">指令碼概觀</span><span class="sxs-lookup"><span data-stu-id="5ae35-125">Script overview</span></span>
<span data-ttu-id="5ae35-126">hello 指令碼範例會安裝 （包括設定無訊息安裝的 MySQL） LAMP 堆疊 tooUbuntu、 將簡單的 PHP 檔案，並啟動 Apache。</span><span class="sxs-lookup"><span data-stu-id="5ae35-126">hello script example installs a LAMP stack tooUbuntu (including setting up a silent install of MySQL), writes a simple PHP file, and starts Apache.</span></span>

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

### <a name="upload-script"></a><span data-ttu-id="5ae35-127">上傳指令碼</span><span class="sxs-lookup"><span data-stu-id="5ae35-127">Upload script</span></span>
<span data-ttu-id="5ae35-128">將 hello 指令碼儲存為文字檔案，例如*install_lamp.sh*，然後再上載 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="5ae35-128">Save hello script as a text file, for example *install_lamp.sh*, and then upload it tooAzure Storage.</span></span> <span data-ttu-id="5ae35-129">您可以使用 Azure CLI，輕鬆執行這個動作。</span><span class="sxs-lookup"><span data-stu-id="5ae35-129">You can do this easily with Azure CLI.</span></span> <span data-ttu-id="5ae35-130">hello 下列範例會上傳 hello 檔案 tooa 儲存體容器名稱為 「 指令碼 」。</span><span class="sxs-lookup"><span data-stu-id="5ae35-130">hello following example uploads hello file tooa storage container named "scripts".</span></span> <span data-ttu-id="5ae35-131">如果 hello 容器不存在，您將需要 toocreate 它第一次。</span><span class="sxs-lookup"><span data-stu-id="5ae35-131">If hello container doesn't exist you'll need toocreate it first.</span></span>

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

<span data-ttu-id="5ae35-132">也會建立描述 toodownload hello 從 Azure 儲存體的指令碼的方式在 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="5ae35-132">Also create a JSON file that describes how toodownload hello script from Azure Storage.</span></span> <span data-ttu-id="5ae35-133">儲存為*public_config.json* （取代"mystorage"hello 您的儲存體帳戶名稱）：</span><span class="sxs-lookup"><span data-stu-id="5ae35-133">Save this as *public_config.json* (replacing "mystorage" with hello name of your storage account):</span></span>

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-hello-extension"></a><span data-ttu-id="5ae35-134">Hello 延伸模組部署</span><span class="sxs-lookup"><span data-stu-id="5ae35-134">Deploy hello extension</span></span>
<span data-ttu-id="5ae35-135">現在您可以使用 hello 下一個命令 toodeploy hello Linux CustomScript 延伸模組 toohello 遠端 VM 使用 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="5ae35-135">Now you can use hello next command toodeploy hello Linux CustomScript Extension toohello remote VM using hello Azure CLI.</span></span>

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

<span data-ttu-id="5ae35-136">hello 前一個命令會下載並執行 hello *install_lamp.sh*指令碼的 VM 稱為的 hello*燈 vm*。</span><span class="sxs-lookup"><span data-stu-id="5ae35-136">hello previous command downloads and runs hello *install_lamp.sh* script on hello VM called *lamp-vm*.</span></span>

<span data-ttu-id="5ae35-137">因為 hello 應用程式包含 web 伺服器，請記住 tooopen HTTP 接聽連接埠上 hello 遠端 VM 與 hello 下一個命令。</span><span class="sxs-lookup"><span data-stu-id="5ae35-137">Since hello app includes a web server, remember tooopen an HTTP listening port on hello remote VM with hello next command.</span></span>

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="5ae35-138">監視與疑難排解</span><span class="sxs-lookup"><span data-stu-id="5ae35-138">Monitoring and troubleshooting</span></span>
<span data-ttu-id="5ae35-139">您可以檢查 hello 自訂的指令碼會藉由查看 hello 記錄檔上 hello 遠端 VM 的程度。</span><span class="sxs-lookup"><span data-stu-id="5ae35-139">You can check on how well hello custom script runs by looking at hello log file on hello remote VM.</span></span> <span data-ttu-id="5ae35-140">SSH 太*燈 vm*和結尾 hello 記錄檔與 hello 下一個命令。</span><span class="sxs-lookup"><span data-stu-id="5ae35-140">SSH too*lamp-vm* and tail hello log file with hello next command.</span></span>

    cd /var/log/azure/customscript
    tail -f handler.log

<span data-ttu-id="5ae35-141">執行 hello CustomScript 延伸模組之後，您可以瀏覽 toohello PHP 頁面，您建立的資訊。</span><span class="sxs-lookup"><span data-stu-id="5ae35-141">After you run hello CustomScript Extension, you can browse toohello PHP page you created for information.</span></span> <span data-ttu-id="5ae35-142">hello PHP 頁面上的這篇文章中的 hello 範例*http://lamp-vm.cloudapp.net/phpinfo.php*。</span><span class="sxs-lookup"><span data-stu-id="5ae35-142">hello PHP page for hello example in this article is *http://lamp-vm.cloudapp.net/phpinfo.php*.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5ae35-143">其他資源</span><span class="sxs-lookup"><span data-stu-id="5ae35-143">Additional resources</span></span>
<span data-ttu-id="5ae35-144">您可以使用 hello 相同的基本步驟 toodeploy 更複雜的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5ae35-144">You can use hello same basic steps toodeploy more complex apps.</span></span> <span data-ttu-id="5ae35-145">在此範例中 hello 安裝指令碼已儲存為 Azure 儲存體中的公用 blob。</span><span class="sxs-lookup"><span data-stu-id="5ae35-145">In this example hello install script was saved as a public blob in Azure Storage.</span></span> <span data-ttu-id="5ae35-146">較安全的選項會是 toostore hello 安裝指令碼為安全的 blob 與[安全的存取簽章](https://msdn.microsoft.com/library/azure/ee395415.aspx)(SAS)。</span><span class="sxs-lookup"><span data-stu-id="5ae35-146">A more secure option would be toostore hello install script as a secure blob with a [Secure Access Signature](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span></span>

<span data-ttu-id="5ae35-147">適用於 Azure CLI、 Linux 和 hello CustomScript 延伸模組的其他資源會列在下一個。</span><span class="sxs-lookup"><span data-stu-id="5ae35-147">Additional resources for Azure CLI, Linux and hello CustomScript Extension are listed next.</span></span>

[<span data-ttu-id="5ae35-148">使用 CustomScript 延伸模組以將 Linux VM 自訂工作自動化</span><span class="sxs-lookup"><span data-stu-id="5ae35-148">Automate Linux VM Customization Tasks Using CustomScript Extension</span></span>](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[<span data-ttu-id="5ae35-149">Azure Linux 延伸模組 (GitHub)</span><span class="sxs-lookup"><span data-stu-id="5ae35-149">Azure Linux Extensions (GitHub)</span></span>](https://github.com/Azure/azure-linux-extensions)