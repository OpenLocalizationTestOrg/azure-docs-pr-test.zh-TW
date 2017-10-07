---
title: "Linux 虛擬機器以 hello Azure CLI 1.0 aaaDeploy 燈 |Microsoft 文件"
description: "了解 Azure 中的 Linux VM 上 tooinstall hello LAMP 堆疊的方式"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jluk
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: NA
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: e78a82d388ce68710933b9b673aa1b2460bdbb14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-with-hello-azure-cli-10"></a><span data-ttu-id="33ac3-103">部署以 hello Azure CLI 1.0 LAMP 堆疊</span><span class="sxs-lookup"><span data-stu-id="33ac3-103">Deploy LAMP stack with hello Azure CLI 1.0</span></span>
<span data-ttu-id="33ac3-104">本文將告訴您如何 toodeploy Apache web 伺服器、 MySQL 和 Azure 上的 PHP （hello LAMP 堆疊）。</span><span class="sxs-lookup"><span data-stu-id="33ac3-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on Azure.</span></span> <span data-ttu-id="33ac3-105">您需要 Azure 帳戶 ([取得免費試用](https://azure.microsoft.com/pricing/free-trial/)) 和 hello [Azure CLI](../../cli-install-nodejs.md)也就是[連接 tooyour Azure 帳戶](../../xplat-cli-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="33ac3-105">You need an Azure Account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and hello [Azure CLI](../../cli-install-nodejs.md) that is [connected tooyour Azure account](../../xplat-cli-connect.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="33ac3-106">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="33ac3-106">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="33ac3-107">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="33ac3-107">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="33ac3-108">[Azure CLI 1.0] – 我們 CLI hello 傳統和資源管理部署模型 （此文件）</span><span class="sxs-lookup"><span data-stu-id="33ac3-108">[Azure CLI 1.0] – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="33ac3-109">[Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -hello 資源管理部署模型我們下一個層代 CLI</span><span class="sxs-lookup"><span data-stu-id="33ac3-109">[Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

```
# One command toocreate a resource group holding a VM with LAMP already on it
$ azure group create -n uniqueResourceGroup -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
```

* <span data-ttu-id="33ac3-110">在現有 VM 上部署 LAMP</span><span class="sxs-lookup"><span data-stu-id="33ac3-110">Deploy LAMP on existing VM</span></span>

```
# Two commands: one updates packages, hello other installs Apache, MySQL, and PHP
user@ubuntu$ sudo apt-get update
user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="33ac3-111">逐步解說在新的 VM 上部署 LAMP</span><span class="sxs-lookup"><span data-stu-id="33ac3-111">Deploy LAMP on new VM walkthrough</span></span>
<span data-ttu-id="33ac3-112">您可以藉由建立啟動[資源群組](../../azure-resource-manager/resource-group-overview.md)，就會包含 hello 新的 VM:</span><span class="sxs-lookup"><span data-stu-id="33ac3-112">You can start by creating a [resource group](../../azure-resource-manager/resource-group-overview.md) that will contain hello new VM:</span></span>

    $ azure group create uniqueResourceGroup westus
    info:    Executing command group create
    info:    Getting resource group uniqueResourceGroup
    info:    Creating resource group uniqueResourceGroup
    info:    Created resource group uniqueResourceGroup
    data:    Id:                  /subscriptions/########-####-####-####-############/resourceGroups/uniqueResourceGroup
    data:    Name:                uniqueResourceGroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags: null
    data:
    info:    group create command OK

<span data-ttu-id="33ac3-113">toocreate hello VM 本身，您可以使用已撰寫的 Azure Resource Manager 範本，找到[這裡 GitHub 上](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app)。</span><span class="sxs-lookup"><span data-stu-id="33ac3-113">toocreate hello VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

    $ azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json uniqueResourceGroup uniqueLampName

<span data-ttu-id="33ac3-114">您應會看到提示更多輸入的回應︰</span><span class="sxs-lookup"><span data-stu-id="33ac3-114">You should see a response prompting some more inputs:</span></span>

    info:    Executing command group deployment create
    info:    Supply values for hello following parameters
    storageAccountNamePrefix: lampprefix
    location: westus
    adminUsername: someUsername
    adminPassword: somePassword
    mySqlPassword: somePassword
    dnsLabelPrefix: azlamptest
    info:    Initializing template configurations and parameters
    info:    Creating a deployment
    info:    Created template deployment "uniqueLampName"
    info:    Waiting for deployment toocomplete
    data:    DeploymentName     : uniqueLampName
    data:    ResourceGroupName  : uniqueResourceGroup
    data:    ProvisioningState  : Succeeded
    data:    Timestamp          :
    data:    Mode               : Incremental
    data:    CorrelationId      : d51bbf3c-88f1-4cf3-a8b3-942c6925f381
    data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
    data:    ContentVersion     : 1.0.0.0
    data:    DeploymentParameters :
    data:    Name                      Type          Value
    data:    ------------------------  ------------  -----------
    data:    storageAccountNamePrefix  String        lampprefix
    data:    location                  String        westus
    data:    adminUsername             String        someUsername
    data:    adminPassword             SecureString  undefined
    data:    mySqlPassword             SecureString  undefined
    data:    dnsLabelPrefix            String        azlamptest
    data:    ubuntuOSVersion           String        14.04.2-LTS
    info:    group deployment create command OK

<span data-ttu-id="33ac3-115">您現在已建立安裝了 LAMP 的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="33ac3-115">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="33ac3-116">如果您希望，您可以確認 hello 安裝太跳躍向[確認燈安裝成功](#verify-lamp-successfully-installed)。</span><span class="sxs-lookup"><span data-stu-id="33ac3-116">If you wish, you can verify hello install by jumping down too[Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="33ac3-117">逐步解說在現有 VM 上部署 LAMP</span><span class="sxs-lookup"><span data-stu-id="33ac3-117">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="33ac3-118">如果您需要協助建立 Linux VM，您可以向[這裡 toolearn 如何 toocreate Linux VM](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="33ac3-118">If you need help creating a Linux VM, you can head [here toolearn how toocreate a Linux VM](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="33ac3-119">接下來，您需要 tooSSH 到 hello Linux VM。</span><span class="sxs-lookup"><span data-stu-id="33ac3-119">Next, you need tooSSH into hello Linux VM.</span></span> <span data-ttu-id="33ac3-120">如果您需要協助建立 SSH 金鑰，您可以向[這裡 toolearn 如何 toocreate Linux/Mac 上的 SSH 金鑰](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="33ac3-120">If you need help with creating an SSH key, you can head [here toolearn how toocreate an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="33ac3-121">如果您已經有 SSH 金鑰，請繼續進行，並從您的命令列透過 SSH 使用 `ssh exampleUsername@exampleDNS` 登入 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="33ac3-121">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh exampleUsername@exampleDNS`.</span></span>

<span data-ttu-id="33ac3-122">現在，您使用 Linux VM 內，我們可以逐步完成安裝 hello LAMP 堆疊 Debian 為基礎的發佈。</span><span class="sxs-lookup"><span data-stu-id="33ac3-122">Now that you are working within your Linux VM, we can walk through installing hello LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="33ac3-123">hello 確實命令可能會與針對其他 Linux 散發版本不同。</span><span class="sxs-lookup"><span data-stu-id="33ac3-123">hello exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="33ac3-124">安裝在 Debian/Ubuntu 上</span><span class="sxs-lookup"><span data-stu-id="33ac3-124">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="33ac3-125">您需要下列安裝套件的 hello: `apache2`， `mysql-server`， `php5`，和`php5-mysql`。</span><span class="sxs-lookup"><span data-stu-id="33ac3-125">You need hello following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="33ac3-126">直接擷取這些封裝或使用 Tasksel，即可安裝這些封裝。</span><span class="sxs-lookup"><span data-stu-id="33ac3-126">You can install these packages by directly grabbing these packages or using Tasksel.</span></span> <span data-ttu-id="33ac3-127">這兩個選項的指示如下所列。</span><span class="sxs-lookup"><span data-stu-id="33ac3-127">Instructions for both options are listed below.</span></span>
<span data-ttu-id="33ac3-128">安裝之前，您需要 toodownload 並更新封裝清單。</span><span class="sxs-lookup"><span data-stu-id="33ac3-128">Before installing you need toodownload and update package lists.</span></span>

    user@ubuntu$ sudo apt-get update

##### <a name="individual-packages"></a><span data-ttu-id="33ac3-129">個別封裝</span><span class="sxs-lookup"><span data-stu-id="33ac3-129">Individual packages</span></span>
<span data-ttu-id="33ac3-130">使用 apt-get：</span><span class="sxs-lookup"><span data-stu-id="33ac3-130">Using apt-get:</span></span>

    user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql

##### <a name="using-tasksel"></a><span data-ttu-id="33ac3-131">使用 Tasksel</span><span class="sxs-lookup"><span data-stu-id="33ac3-131">Using tasksel</span></span>
<span data-ttu-id="33ac3-132">或者，您也可以下載 Tasksel，這是一個 Debian/Ubuntu 工具，以協調工作的方式安裝多個相關套件到您的系統上。</span><span class="sxs-lookup"><span data-stu-id="33ac3-132">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

    user@ubuntu$ sudo apt-get install tasksel
    user@ubuntu$ sudo tasksel install lamp-server

<span data-ttu-id="33ac3-133">後執行的其中一個 hello 上述選項，您將會被提示的 tooinstall，這些封裝和各種其他相依性。</span><span class="sxs-lookup"><span data-stu-id="33ac3-133">After running either of hello previous options, you will be prompted tooinstall these packages and various other dependencies.</span></span> <span data-ttu-id="33ac3-134">按 'y' 'Enter' toocontinue，並遵循 MySQL 任何其他提示 tooset 系統管理密碼。</span><span class="sxs-lookup"><span data-stu-id="33ac3-134">Press 'y' and then 'Enter' toocontinue, and follow any other prompts tooset an administrative password for MySQL.</span></span> <span data-ttu-id="33ac3-135">這會 hello 最小必要的 PHP 延伸模組需要 toouse PHP 安裝 MySQL。</span><span class="sxs-lookup"><span data-stu-id="33ac3-135">This installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="33ac3-136">執行下列命令 toosee hello 封裝其他 PHP 延伸模組：</span><span class="sxs-lookup"><span data-stu-id="33ac3-136">Run hello following command toosee other PHP extensions that are available as packages:</span></span>

    user@ubuntu$ apt-cache search php5


#### <a name="create-infophp-document"></a><span data-ttu-id="33ac3-137">建立 info.php 文件</span><span class="sxs-lookup"><span data-stu-id="33ac3-137">Create info.php document</span></span>
<span data-ttu-id="33ac3-138">您現在應該能夠 toocheck Apache、 MySQL 和 PHP 您擁有版本透過 hello 命令列輸入`apache2 -v`， `mysql -v`，或`php -v`。</span><span class="sxs-lookup"><span data-stu-id="33ac3-138">You should now be able toocheck what version of Apache, MySQL, and PHP you have through hello command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="33ac3-139">如果您將像是 tootest 此外，您可以建立快速的 PHP 資訊頁面 tooview 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="33ac3-139">If you would like tootest further, you can create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="33ac3-140">透過以下命令，使用 Nano 文字編輯器建立檔案：</span><span class="sxs-lookup"><span data-stu-id="33ac3-140">Create a file with Nano text editor with this command:</span></span>

    user@ubuntu$ sudo nano /var/www/html/info.php

<span data-ttu-id="33ac3-141">在 hello GNU Nano 文字編輯器 中，加入下列行 hello:</span><span class="sxs-lookup"><span data-stu-id="33ac3-141">Within hello GNU Nano text editor, add hello following lines:</span></span>

    <?php
    phpinfo();
    ?>

<span data-ttu-id="33ac3-142">然後，儲存並結束 hello 文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="33ac3-142">Then save and exit hello text editor.</span></span>

<span data-ttu-id="33ac3-143">使用這個命令重新啟動 Apache，讓所有新的安裝生效。</span><span class="sxs-lookup"><span data-stu-id="33ac3-143">Restart Apache with this command so all new installs take effect.</span></span>

    user@ubuntu$ sudo service apache2 restart

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="33ac3-144">確認 LAMP 安裝成功</span><span class="sxs-lookup"><span data-stu-id="33ac3-144">Verify LAMP successfully installed</span></span>
<span data-ttu-id="33ac3-145">現在您可以檢查您建立開啟瀏覽器並移 toohttp://youruniqueDNS/info.php hello PHP 資訊頁面。</span><span class="sxs-lookup"><span data-stu-id="33ac3-145">Now you can check hello PHP info page you created by opening a browser and going toohttp://youruniqueDNS/info.php.</span></span> <span data-ttu-id="33ac3-146">它看起來應該類似 toothis 映像。</span><span class="sxs-lookup"><span data-stu-id="33ac3-146">It should look similar toothis image.</span></span>

![][2]

<span data-ttu-id="33ac3-147">您可以檢查您的 Apache 安裝移 tooyou http://youruniqueDNS/ 檢視 hello Apache2 Ubuntu 預設頁面。</span><span class="sxs-lookup"><span data-stu-id="33ac3-147">You can check your Apache installation by viewing hello Apache2 Ubuntu Default Page by going tooyou http://youruniqueDNS/.</span></span> <span data-ttu-id="33ac3-148">您應該會看到類似下圖的內容。</span><span class="sxs-lookup"><span data-stu-id="33ac3-148">You should see something like this image.</span></span>

![][3]

<span data-ttu-id="33ac3-149">恭喜，您剛已在 Azure VM 上安裝 LAMP 堆疊！</span><span class="sxs-lookup"><span data-stu-id="33ac3-149">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="33ac3-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="33ac3-150">Next steps</span></span>
<span data-ttu-id="33ac3-151">簽出 hello hello LAMP 堆疊上的 Ubuntu 文件：</span><span class="sxs-lookup"><span data-stu-id="33ac3-151">Check out hello Ubuntu documentation on hello LAMP stack:</span></span>

* [<span data-ttu-id="33ac3-152">https://help.ubuntu.com/community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="33ac3-152">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png