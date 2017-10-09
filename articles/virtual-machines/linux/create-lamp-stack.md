---
title: "在 Azure 中 Linux 虛擬機器上的燈 aaaDeploy |Microsoft 文件"
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
ms.devlang: azurecli
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: 42d887bb9f78becc02505e336be25fdaaf78df70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-on-azure"></a><span data-ttu-id="1848f-103">在 Azure 上部署 LAMP 堆疊</span><span class="sxs-lookup"><span data-stu-id="1848f-103">Deploy LAMP stack on Azure</span></span>
<span data-ttu-id="1848f-104">本文將告訴您如何 toodeploy Apache web 伺服器、 MySQL 和 Azure 上的 PHP （hello LAMP 堆疊）。</span><span class="sxs-lookup"><span data-stu-id="1848f-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on Azure.</span></span> <span data-ttu-id="1848f-105">您需要 Azure 帳戶 ([取得免費試用](https://azure.microsoft.com/pricing/free-trial/)) 和 hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)。</span><span class="sxs-lookup"><span data-stu-id="1848f-105">You need an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span> <span data-ttu-id="1848f-106">您也可以執行下列步驟以 hello [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="1848f-106">You can also perform these steps with hello [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="1848f-107">快速命令摘要</span><span class="sxs-lookup"><span data-stu-id="1848f-107">Quick command summary</span></span>

1. <span data-ttu-id="1848f-108">儲存並編輯 hello [azuredeploy.parameters.json 檔案](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json)tooyour 喜好設定，在本機電腦上的。</span><span class="sxs-lookup"><span data-stu-id="1848f-108">Save and edit hello [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour preference on your local machine.</span></span>
2. <span data-ttu-id="1848f-109">執行下列兩個命令 toocreate hello 資源群組，然後再部署您的範本：</span><span class="sxs-lookup"><span data-stu-id="1848f-109">Run hello following two commands toocreate a resource group and then deploy your template:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a><span data-ttu-id="1848f-110">在現有 VM 上部署 LAMP</span><span class="sxs-lookup"><span data-stu-id="1848f-110">Deploy LAMP on existing VM</span></span>
<span data-ttu-id="1848f-111">hello 下列安裝 Apache、 MySQL 和 PHP，接著更新封裝的命令：</span><span class="sxs-lookup"><span data-stu-id="1848f-111">hello following commands updates packages, then installs Apache, MySQL, and PHP:</span></span>

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="1848f-112">逐步解說在新的 VM 上部署 LAMP</span><span class="sxs-lookup"><span data-stu-id="1848f-112">Deploy LAMP on new VM walkthrough</span></span>

1. <span data-ttu-id="1848f-113">建立資源群組與[az 群組建立](/cli/azure/group#create)toocontain hello 新的 VM:</span><span class="sxs-lookup"><span data-stu-id="1848f-113">Create a resource group with [az group create](/cli/azure/group#create) toocontain hello new VM:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
```
<span data-ttu-id="1848f-114">toocreate hello VM 本身，您可以使用已撰寫的 Azure Resource Manager 範本，找到[這裡 GitHub 上](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app)。</span><span class="sxs-lookup"><span data-stu-id="1848f-114">toocreate hello VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

2. <span data-ttu-id="1848f-115">儲存 hello [azuredeploy.parameters.json 檔案](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json)tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="1848f-115">Save hello [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour local machine.</span></span>
3. <span data-ttu-id="1848f-116">編輯 hello **azuredeploy.parameters.json**檔案 tooyour 慣用的輸入。</span><span class="sxs-lookup"><span data-stu-id="1848f-116">Edit hello **azuredeploy.parameters.json** file tooyour preferred inputs.</span></span>
4. <span data-ttu-id="1848f-117">部署與 hello 範本 [az 群組部署建立] 參考 hello 下載 json 檔案：</span><span class="sxs-lookup"><span data-stu-id="1848f-117">Deploy hello template with [az group deployment create] referencing hello downloaded json file:</span></span>

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

<span data-ttu-id="1848f-118">hello 輸出是 toohello 類似下列範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="1848f-118">hello output is similar toohello following example:</span></span>

```json
{
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup/providers/Microsoft.Resources/deployments/azuredeploy",
"name": "azuredeploy",
"properties": {
    "correlationId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "debugSetting": null,
}
...
"provisioningState": "Succeeded",
"template": null,
"templateLink": {
    "contentVersion": "1.0.0.0",
    "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json"
    },
    "timestamp": "2017-02-22T00:05:51.860411+00:00"
},
"resourceGroup": "myResourceGroup"
}
```

<span data-ttu-id="1848f-119">您現在已建立安裝了 LAMP 的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="1848f-119">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="1848f-120">如果您希望，您可以確認 hello 安裝太跳躍向[確認燈安裝成功](#verify-lamp-successfully-installed)。</span><span class="sxs-lookup"><span data-stu-id="1848f-120">If you wish, you can verify hello install by jumping down too[Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="1848f-121">逐步解說在現有 VM 上部署 LAMP</span><span class="sxs-lookup"><span data-stu-id="1848f-121">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="1848f-122">如果您需要協助建立 Linux VM，您可以向[這裡 toolearn 如何 toocreate Linux VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli)。</span><span class="sxs-lookup"><span data-stu-id="1848f-122">If you need help creating a Linux VM, you can head [here toolearn how toocreate a Linux VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span></span> <span data-ttu-id="1848f-123">接下來，您需要 tooSSH 到 hello Linux VM。</span><span class="sxs-lookup"><span data-stu-id="1848f-123">Next, you need tooSSH into hello Linux VM.</span></span> <span data-ttu-id="1848f-124">如果您需要協助建立 SSH 金鑰，您可以向[這裡 toolearn 如何 toocreate Linux/Mac 上的 SSH 金鑰](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="1848f-124">If you need help with creating an SSH key, you can head [here toolearn how toocreate an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="1848f-125">如果您已經有 SSH 金鑰，請繼續進行，並從您的命令列透過 SSH 使用 `ssh azureuser@mypublicdns.westus.cloudapp.azure.com` 登入 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="1848f-125">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="1848f-126">現在，您使用 Linux VM 內，我們可以逐步完成安裝 hello LAMP 堆疊 Debian 為基礎的發佈。</span><span class="sxs-lookup"><span data-stu-id="1848f-126">Now that you are working within your Linux VM, we can walk through installing hello LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="1848f-127">hello 確實命令可能會與針對其他 Linux 散發版本不同。</span><span class="sxs-lookup"><span data-stu-id="1848f-127">hello exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="1848f-128">安裝在 Debian/Ubuntu 上</span><span class="sxs-lookup"><span data-stu-id="1848f-128">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="1848f-129">您需要下列安裝套件的 hello: `apache2`， `mysql-server`， `php5`，和`php5-mysql`。</span><span class="sxs-lookup"><span data-stu-id="1848f-129">You need hello following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="1848f-130">直接擷取這些封裝或使用 Tasksel，即可安裝這些封裝。</span><span class="sxs-lookup"><span data-stu-id="1848f-130">You can install these packages by directly grabbing these packages or using Tasksel.</span></span>
<span data-ttu-id="1848f-131">安裝之前，您需要 toodownload 並更新封裝清單。</span><span class="sxs-lookup"><span data-stu-id="1848f-131">Before installing you need toodownload and update package lists.</span></span>

```bash
sudo apt-get update
```

##### <a name="individual-packages"></a><span data-ttu-id="1848f-132">個別封裝</span><span class="sxs-lookup"><span data-stu-id="1848f-132">Individual packages</span></span>
<span data-ttu-id="1848f-133">使用 apt-get：</span><span class="sxs-lookup"><span data-stu-id="1848f-133">Using apt-get:</span></span>

```bash
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

##### <a name="using-tasksel"></a><span data-ttu-id="1848f-134">使用 Tasksel</span><span class="sxs-lookup"><span data-stu-id="1848f-134">Using tasksel</span></span>
<span data-ttu-id="1848f-135">或者，您也可以下載 Tasksel，這是一個 Debian/Ubuntu 工具，以協調工作的方式安裝多個相關套件到您的系統上。</span><span class="sxs-lookup"><span data-stu-id="1848f-135">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

```bash
sudo apt-get install tasksel
sudo tasksel install lamp-server
```

<span data-ttu-id="1848f-136">後執行的其中一個 hello 上述選項，您將會被提示的 tooinstall，這些封裝和各種其他相依性。</span><span class="sxs-lookup"><span data-stu-id="1848f-136">After running either of hello previous options, you will be prompted tooinstall these packages and various other dependencies.</span></span> <span data-ttu-id="1848f-137">按 'y' 'Enter' toocontinue tooset MySQL 的系統管理密碼，並依照任何其他提示。</span><span class="sxs-lookup"><span data-stu-id="1848f-137">tooset an administrative password for MySQL, press 'y' and then 'Enter' toocontinue, and follow any other prompts.</span></span> <span data-ttu-id="1848f-138">此程序會 hello 最小必要的 PHP 延伸模組需要 toouse PHP 安裝 MySQL。</span><span class="sxs-lookup"><span data-stu-id="1848f-138">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="1848f-139">執行下列命令 toosee hello 封裝其他 PHP 延伸模組：</span><span class="sxs-lookup"><span data-stu-id="1848f-139">Run hello following command toosee other PHP extensions that are available as packages:</span></span>

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a><span data-ttu-id="1848f-140">建立 info.php 文件</span><span class="sxs-lookup"><span data-stu-id="1848f-140">Create info.php document</span></span>
<span data-ttu-id="1848f-141">您現在應該能夠 toocheck Apache、 MySQL 和 PHP 您擁有版本透過 hello 命令列輸入`apache2 -v`， `mysql -v`，或`php -v`。</span><span class="sxs-lookup"><span data-stu-id="1848f-141">You should now be able toocheck what version of Apache, MySQL, and PHP you have through hello command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="1848f-142">如果您將像是 tootest 此外，您可以建立快速的 PHP 資訊頁面 tooview 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="1848f-142">If you would like tootest further, you can create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="1848f-143">透過以下命令，使用 Nano 文字編輯器建立檔案：</span><span class="sxs-lookup"><span data-stu-id="1848f-143">Create a file with Nano text editor with this command:</span></span>

```bash
sudo nano /var/www/html/info.php
```

<span data-ttu-id="1848f-144">在 hello GNU Nano 文字編輯器 中，加入下列行 hello:</span><span class="sxs-lookup"><span data-stu-id="1848f-144">Within hello GNU Nano text editor, add hello following lines:</span></span>

```php
<?php
phpinfo();
?>
```

<span data-ttu-id="1848f-145">然後，儲存並結束 hello 文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="1848f-145">Then save and exit hello text editor.</span></span>

<span data-ttu-id="1848f-146">使用這個命令重新啟動 Apache，讓所有新的安裝生效。</span><span class="sxs-lookup"><span data-stu-id="1848f-146">Restart Apache with this command so all new installs take effect.</span></span>

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="1848f-147">確認 LAMP 安裝成功</span><span class="sxs-lookup"><span data-stu-id="1848f-147">Verify LAMP successfully installed</span></span>
<span data-ttu-id="1848f-148">現在您可以檢查您建立開啟瀏覽器並移 toohttp://youruniqueDNS/info.php hello PHP 資訊頁面。</span><span class="sxs-lookup"><span data-stu-id="1848f-148">Now you can check hello PHP info page you created by opening a browser and going toohttp://youruniqueDNS/info.php.</span></span> <span data-ttu-id="1848f-149">它看起來應該類似 toothis 映像。</span><span class="sxs-lookup"><span data-stu-id="1848f-149">It should look similar toothis image.</span></span>

![][2]

<span data-ttu-id="1848f-150">您可以檢查您的 Apache 安裝移 tooyou http://youruniqueDNS/ 檢視 hello Apache2 Ubuntu 預設頁面。</span><span class="sxs-lookup"><span data-stu-id="1848f-150">You can check your Apache installation by viewing hello Apache2 Ubuntu Default Page by going tooyou http://youruniqueDNS/.</span></span> <span data-ttu-id="1848f-151">hello 輸出是 toohello 類似下列範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="1848f-151">hello output is similar toohello following example:</span></span>

![][3]

<span data-ttu-id="1848f-152">恭喜，您剛已在 Azure VM 上安裝 LAMP 堆疊！</span><span class="sxs-lookup"><span data-stu-id="1848f-152">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="1848f-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1848f-153">Next steps</span></span>
<span data-ttu-id="1848f-154">簽出 hello hello LAMP 堆疊上的 Ubuntu 文件：</span><span class="sxs-lookup"><span data-stu-id="1848f-154">Check out hello Ubuntu documentation on hello LAMP stack:</span></span>

* [<span data-ttu-id="1848f-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="1848f-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png
