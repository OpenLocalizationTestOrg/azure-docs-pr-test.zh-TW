---
title: "在 Linux VM 上使用 CustomScript 擴充功能 | Microsoft Docs"
description: "了解如何使用 CustomScript 擴充功能，在 Azure 中以傳統部署模型所建立的 Linux 虛擬機器上部署應用程式。"
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
ms.openlocfilehash: cb1fc9a44dc9e57d9cc9f1c546ad937d67e63c2f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-lamp-app-using-the-azure-customscript-extension-for-linux"></a><span data-ttu-id="fdb7e-103">使用適用於 Linux 的 Azure CustomScript 延伸模組部署 LAMP 應用程式</span><span class="sxs-lookup"><span data-stu-id="fdb7e-103">Deploy a LAMP app using the Azure CustomScript Extension for Linux</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="fdb7e-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fdb7e-105">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="fdb7e-106">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="fdb7e-107">如需使用 Resource Manager 模型部署 LAMP 堆疊的詳細資訊，請參閱[這裡](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-107">For information about deploying a LAMP stack using the Resource Manager model, see [here](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="fdb7e-108">適用於 Linux 的 Microsoft Azure CustomScript 延伸模組提供一種方式，讓您可以執行使用該虛擬機器 (VM) 所支援的任何指令碼語言 (例如 Python 和 Bash) 所撰寫的任意程式碼來自訂 VM。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-108">The Microsoft Azure CustomScript Extension for Linux provides a way to customize your virtual machines (VMs) by running arbitrary code written in any scripting language supported by the VM (for example, Python, and Bash).</span></span> <span data-ttu-id="fdb7e-109">這提供極具彈性的方式，自動將應用程式部署到多部電腦。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-109">This provides a very flexible way to automate application deployment to multiple machines.</span></span>

<span data-ttu-id="fdb7e-110">您可以使用 Azure 入口網站、Windows PowerShell 或 Azure 命令列介面 (Azure CLI)，來部署 CustomScript 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-110">You can deploy the CustomScript Extension using the Azure portal, Windows PowerShell, or the Azure Command-Line Interface (Azure CLI).</span></span>

<span data-ttu-id="fdb7e-111">在本文中我們將使用 Azure CLI，將簡單的 LAMP 應用程式部署至以傳統部署模型建立的 Ubuntu VM。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-111">In this article we'll use the Azure CLI to deploy a simple LAMP application to an Ubuntu VM created using the classic deployment model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fdb7e-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="fdb7e-112">Prerequisites</span></span>
<span data-ttu-id="fdb7e-113">在此範例中，會先建立兩個執行 Ubuntu 14.04 或更新版本的 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-113">For this example, first create two Azure VMs running Ubuntu 14.04 or later.</span></span> <span data-ttu-id="fdb7e-114">VM 的名稱為 script-vm 和 lamp-vm。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-114">The VMs are called *script-vm* and *lamp-vm*.</span></span> <span data-ttu-id="fdb7e-115">建立 VM 時請使用唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-115">Use unique names when you create the VMs.</span></span> <span data-ttu-id="fdb7e-116">其中一個用來執行 CLI 命令，而另一個用來部署 LAMP 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-116">One is used to run the CLI commands and one is used to deploy the LAMP app.</span></span>

<span data-ttu-id="fdb7e-117">您也需要 Azure 儲存體帳戶和金鑰才能存取它 (您可以從 Azure 入口網站取得此資訊)。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-117">You also need an Azure Storage account and a key to access it (you can get this from the Azure portal).</span></span>

<span data-ttu-id="fdb7e-118">如果您需要在 Azure 上建立 Linux VM 的說明，請參閱[建立執行 Linux 的虛擬機器](createportal.md)。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-118">If you need help creating Linux VMs on Azure refer to [Create a Virtual Machine Running Linux](createportal.md).</span></span>

<span data-ttu-id="fdb7e-119">安裝命令假設的是 Ubuntu，但是您可以對任何支援的 Linux distro 採用此安裝。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-119">The install commands assume Ubuntu, but you can adapt the installation for any supported Linux distro.</span></span>

<span data-ttu-id="fdb7e-120">script-vm VM 需要安裝 Azure CLI，並且與 Azure 之間具有正常運作的連線。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-120">The script-vm VM needs to have Azure CLI installed, with a working connection to Azure.</span></span> <span data-ttu-id="fdb7e-121">如需此動作的說明，請參閱 [安裝與設定 Azure 命令列介面](../../../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-121">For help with this refer to [Install and Configure the Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span>

## <a name="upload-a-script"></a><span data-ttu-id="fdb7e-122">上傳指令碼</span><span class="sxs-lookup"><span data-stu-id="fdb7e-122">Upload a script</span></span>
<span data-ttu-id="fdb7e-123">我們會使用 CustomScript 擴充功能在遠端 VM 上執行指令碼，以安裝 LAMP 堆疊並建立 PHP 頁面。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-123">We'll use the CustomScript Extension to run a script on a remote VM to install the LAMP stack and create a PHP page.</span></span> <span data-ttu-id="fdb7e-124">為了可從任何地方存取指令碼，我們會以 Azure Blob 形式上傳該指令碼。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-124">In order to access the script from anywhere we'll upload it as an Azure blob.</span></span>

### <a name="script-overview"></a><span data-ttu-id="fdb7e-125">指令碼概觀</span><span class="sxs-lookup"><span data-stu-id="fdb7e-125">Script overview</span></span>
<span data-ttu-id="fdb7e-126">此指令碼範例會將 LAMP 堆疊安裝到 Ubuntu (包括設定 MySQL 的無訊息安裝)、寫入簡單的 PHP 檔案，並啟動 Apache。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-126">The script example installs a LAMP stack to Ubuntu (including setting up a silent install of MySQL), writes a simple PHP file, and starts Apache.</span></span>

    #!/bin/bash
    # set up a silent install of MySQL
    dbpass="mySQLPassw0rd"

    export DEBIAN_FRONTEND=noninteractive
    echo mysql-server-5.6 mysql-server/root_password password $dbpass | debconf-set-selections
    echo mysql-server-5.6 mysql-server/root_password_again password $dbpass | debconf-set-selections

    # install the LAMP stack
    apt-get -y install apache2 mysql-server php5 php5-mysql  

    # write some PHP
    echo \<center\>\<h1\>My Demo App\</h1\>\<br/\>\</center\> > /var/www/html/phpinfo.php
    echo \<\?php phpinfo\(\)\; \?\> >> /var/www/html/phpinfo.php

    # restart Apache
    apachectl restart

### <a name="upload-script"></a><span data-ttu-id="fdb7e-127">上傳指令碼</span><span class="sxs-lookup"><span data-stu-id="fdb7e-127">Upload script</span></span>
<span data-ttu-id="fdb7e-128">將指令碼儲存為文字檔 (例如 install_lamp.sh)，然後將它上傳到 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-128">Save the script as a text file, for example *install_lamp.sh*, and then upload it to Azure Storage.</span></span> <span data-ttu-id="fdb7e-129">您可以使用 Azure CLI，輕鬆執行這個動作。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-129">You can do this easily with Azure CLI.</span></span> <span data-ttu-id="fdb7e-130">下列範例會將檔案上傳到名為 "scripts" 的儲存體容器中。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-130">The following example uploads the file to a storage container named "scripts".</span></span> <span data-ttu-id="fdb7e-131">如果此容器不存在，您必須先建立它。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-131">If the container doesn't exist you'll need to create it first.</span></span>

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

<span data-ttu-id="fdb7e-132">此外，還會建立 JSON 檔案，此檔案會描述如何從 Azure 儲存體下載指令碼。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-132">Also create a JSON file that describes how to download the script from Azure Storage.</span></span> <span data-ttu-id="fdb7e-133">將此檔案儲存為 public_config.json (使用您的儲存體帳戶名稱來取代 "mystorage")：</span><span class="sxs-lookup"><span data-stu-id="fdb7e-133">Save this as *public_config.json* (replacing "mystorage" with the name of your storage account):</span></span>

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-the-extension"></a><span data-ttu-id="fdb7e-134">部署延伸模組</span><span class="sxs-lookup"><span data-stu-id="fdb7e-134">Deploy the extension</span></span>
<span data-ttu-id="fdb7e-135">現在您可以使用下一個命令，透過 Azure CLI 將 Linux CustomScript 延伸模組部署到遠端 VM。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-135">Now you can use the next command to deploy the Linux CustomScript Extension to the remote VM using the Azure CLI.</span></span>

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

<span data-ttu-id="fdb7e-136">前一個命令會在名為 lamp-vm 的 VM 上下載並執行 install_lamp.sh 指令碼。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-136">The previous command downloads and runs the *install_lamp.sh* script on the VM called *lamp-vm*.</span></span>

<span data-ttu-id="fdb7e-137">因為該應用程式包含 Web 伺服器，所以請記得使用下列命令，在遠端 VM 上開啟 HTTP 接聽連接埠。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-137">Since the app includes a web server, remember to open an HTTP listening port on the remote VM with the next command.</span></span>

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="fdb7e-138">監視與疑難排解</span><span class="sxs-lookup"><span data-stu-id="fdb7e-138">Monitoring and troubleshooting</span></span>
<span data-ttu-id="fdb7e-139">您可以藉由查看遠端 VM 上的記錄檔來檢查自訂指令碼執行的情況。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-139">You can check on how well the custom script runs by looking at the log file on the remote VM.</span></span> <span data-ttu-id="fdb7e-140">SSH 連線到 *lamp-vm* ，並使用下一個命令顯示記錄檔的結尾。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-140">SSH to *lamp-vm* and tail the log file with the next command.</span></span>

    cd /var/log/azure/customscript
    tail -f handler.log

<span data-ttu-id="fdb7e-141">執行 CustomScript 延伸模組之後，您可以瀏覽至您建立的 PHP 網頁以取得資訊。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-141">After you run the CustomScript Extension, you can browse to the PHP page you created for information.</span></span> <span data-ttu-id="fdb7e-142">這篇文章中的範例 PHP 頁面是 *http://lamp-vm.cloudapp.net/phpinfo.php*。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-142">The PHP page for the example in this article is *http://lamp-vm.cloudapp.net/phpinfo.php*.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fdb7e-143">其他資源</span><span class="sxs-lookup"><span data-stu-id="fdb7e-143">Additional resources</span></span>
<span data-ttu-id="fdb7e-144">您可以使用相同的基本步驟來部署更複雜的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-144">You can use the same basic steps to deploy more complex apps.</span></span> <span data-ttu-id="fdb7e-145">此範例將安裝指令碼儲存為 Azure 儲存體中的公用 Blob。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-145">In this example the install script was saved as a public blob in Azure Storage.</span></span> <span data-ttu-id="fdb7e-146">比較安全的選項是使用 [安全存取簽章](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS)，以安全 Blob 形式儲存安裝指令碼。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-146">A more secure option would be to store the install script as a secure blob with a [Secure Access Signature](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span></span>

<span data-ttu-id="fdb7e-147">以下列出 Azure CLI、Linux 與 CustomScript 延伸模組的其他資源。</span><span class="sxs-lookup"><span data-stu-id="fdb7e-147">Additional resources for Azure CLI, Linux and the CustomScript Extension are listed next.</span></span>

[<span data-ttu-id="fdb7e-148">使用 CustomScript 延伸模組以將 Linux VM 自訂工作自動化</span><span class="sxs-lookup"><span data-stu-id="fdb7e-148">Automate Linux VM Customization Tasks Using CustomScript Extension</span></span>](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[<span data-ttu-id="fdb7e-149">Azure Linux 延伸模組 (GitHub)</span><span class="sxs-lookup"><span data-stu-id="fdb7e-149">Azure Linux Extensions (GitHub)</span></span>](https://github.com/Azure/azure-linux-extensions)