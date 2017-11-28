---
title: "在 Azure 的 Linux 虛擬機器上部署 LAMP | Microsoft Docs"
description: "了解如何在 Azure 的 Linux VM 上安裝 LAMP 堆疊"
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
ms.openlocfilehash: ad69876bfbeba5f948a81e5c48c659fdf2265ae2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-lamp-stack-on-azure"></a><span data-ttu-id="03824-103">在 Azure 上部署 LAMP 堆疊</span><span class="sxs-lookup"><span data-stu-id="03824-103">Deploy LAMP stack on Azure</span></span>
<span data-ttu-id="03824-104">本文會逐步引導您在 Azure 上部署 Apache Web 伺服器、MySQL 和 PHP (LAMP 堆疊)。</span><span class="sxs-lookup"><span data-stu-id="03824-104">This article walks you through how to deploy an Apache web server, MySQL, and PHP (the LAMP stack) on Azure.</span></span> <span data-ttu-id="03824-105">您需要 Azure 帳戶 ([取得免費試用](https://azure.microsoft.com/pricing/free-trial/)) 和 [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)。</span><span class="sxs-lookup"><span data-stu-id="03824-105">You need an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and the [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span> <span data-ttu-id="03824-106">您也可以使用 [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 來執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="03824-106">You can also perform these steps with the [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="03824-107">快速命令摘要</span><span class="sxs-lookup"><span data-stu-id="03824-107">Quick command summary</span></span>

1. <span data-ttu-id="03824-108">將 [azuredeploy.parameters.json 檔案](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json)儲存並編輯到本機電腦上的喜好設定。</span><span class="sxs-lookup"><span data-stu-id="03824-108">Save and edit the [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) to your preference on your local machine.</span></span>
2. <span data-ttu-id="03824-109">執行下列兩個命令來建立資源群組，然後部署範本︰</span><span class="sxs-lookup"><span data-stu-id="03824-109">Run the following two commands to create a resource group and then deploy your template:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a><span data-ttu-id="03824-110">在現有 VM 上部署 LAMP</span><span class="sxs-lookup"><span data-stu-id="03824-110">Deploy LAMP on existing VM</span></span>
<span data-ttu-id="03824-111">下列命令會更新套件，然後安裝 Apache、MySQL 和 PHP︰</span><span class="sxs-lookup"><span data-stu-id="03824-111">The following commands updates packages, then installs Apache, MySQL, and PHP:</span></span>

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="03824-112">逐步解說在新的 VM 上部署 LAMP</span><span class="sxs-lookup"><span data-stu-id="03824-112">Deploy LAMP on new VM walkthrough</span></span>

1. <span data-ttu-id="03824-113">使用 [az group create](/cli/azure/group#create) 來建立資源群組以包含新的 VM：</span><span class="sxs-lookup"><span data-stu-id="03824-113">Create a resource group with [az group create](/cli/azure/group#create) to contain the new VM:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
```
<span data-ttu-id="03824-114">若要建立 VM 本身，您可以使用已撰寫的 Azure Resource Manager 範本 (位於 [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app))。</span><span class="sxs-lookup"><span data-stu-id="03824-114">To create the VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

2. <span data-ttu-id="03824-115">將 [azuredeploy.parameters.json 檔案](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json)儲存到本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="03824-115">Save the [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) to your local machine.</span></span>
3. <span data-ttu-id="03824-116">將 **azuredeploy.parameters.json** 檔案編輯到慣用的輸入中。</span><span class="sxs-lookup"><span data-stu-id="03824-116">Edit the **azuredeploy.parameters.json** file to your preferred inputs.</span></span>
4. <span data-ttu-id="03824-117">使用參考所下載 json 檔案的 [az group deployment create] 來部署範本︰</span><span class="sxs-lookup"><span data-stu-id="03824-117">Deploy the template with [az group deployment create] referencing the downloaded json file:</span></span>

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

<span data-ttu-id="03824-118">輸出類似於下列範例：</span><span class="sxs-lookup"><span data-stu-id="03824-118">The output is similar to the following example:</span></span>

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

<span data-ttu-id="03824-119">您現在已建立安裝了 LAMP 的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="03824-119">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="03824-120">如果您希望，您可以向下跳到[確認 LAMP 安裝成功](#verify-lamp-successfully-installed)來確認安裝。</span><span class="sxs-lookup"><span data-stu-id="03824-120">If you wish, you can verify the install by jumping down to [Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="03824-121">逐步解說在現有 VM 上部署 LAMP</span><span class="sxs-lookup"><span data-stu-id="03824-121">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="03824-122">如果您需要建立 Linux VM 的說明，您可以前往[這裡以了解如何建立 Linux VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli)。</span><span class="sxs-lookup"><span data-stu-id="03824-122">If you need help creating a Linux VM, you can head [here to learn how to create a Linux VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span></span> <span data-ttu-id="03824-123">接下來，您需要透過 SSH 登入 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="03824-123">Next, you need to SSH into the Linux VM.</span></span> <span data-ttu-id="03824-124">如果您需要建立 SSH 金鑰的說明，您可以前往[這裡以了解如何在 Linux/Mac 上建立 SSH 金鑰](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="03824-124">If you need help with creating an SSH key, you can head [here to learn how to create an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="03824-125">如果您已經有 SSH 金鑰，請繼續進行，並從您的命令列透過 SSH 使用 `ssh azureuser@mypublicdns.westus.cloudapp.azure.com` 登入 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="03824-125">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="03824-126">您目前正在 Linux VM 內運作，我們可逐步引導您在以 Debian 為基礎的散發版本上安裝 LAMP 堆疊。</span><span class="sxs-lookup"><span data-stu-id="03824-126">Now that you are working within your Linux VM, we can walk through installing the LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="03824-127">其他 Linux 散發版本的確切命令可能會有所不同。</span><span class="sxs-lookup"><span data-stu-id="03824-127">The exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="03824-128">安裝在 Debian/Ubuntu 上</span><span class="sxs-lookup"><span data-stu-id="03824-128">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="03824-129">您需要安裝下列封裝：`apache2`、`mysql-server`、`php5` 和 `php5-mysql`。</span><span class="sxs-lookup"><span data-stu-id="03824-129">You need the following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="03824-130">直接擷取這些封裝或使用 Tasksel，即可安裝這些封裝。</span><span class="sxs-lookup"><span data-stu-id="03824-130">You can install these packages by directly grabbing these packages or using Tasksel.</span></span>
<span data-ttu-id="03824-131">安裝之前，您必須下載並更新封裝清單。</span><span class="sxs-lookup"><span data-stu-id="03824-131">Before installing you need to download and update package lists.</span></span>

```bash
sudo apt-get update
```

##### <a name="individual-packages"></a><span data-ttu-id="03824-132">個別封裝</span><span class="sxs-lookup"><span data-stu-id="03824-132">Individual packages</span></span>
<span data-ttu-id="03824-133">使用 apt-get：</span><span class="sxs-lookup"><span data-stu-id="03824-133">Using apt-get:</span></span>

```bash
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

##### <a name="using-tasksel"></a><span data-ttu-id="03824-134">使用 Tasksel</span><span class="sxs-lookup"><span data-stu-id="03824-134">Using tasksel</span></span>
<span data-ttu-id="03824-135">或者，您也可以下載 Tasksel，這是一個 Debian/Ubuntu 工具，以協調工作的方式安裝多個相關套件到您的系統上。</span><span class="sxs-lookup"><span data-stu-id="03824-135">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

```bash
sudo apt-get install tasksel
sudo tasksel install lamp-server
```

<span data-ttu-id="03824-136">執行上述任一選項之後，隨即會提示您安裝這些封裝和其他各種相依性。</span><span class="sxs-lookup"><span data-stu-id="03824-136">After running either of the previous options, you will be prompted to install these packages and various other dependencies.</span></span> <span data-ttu-id="03824-137">若要設定 MySQL 的管理密碼，請按 [y] 然後按 Enter 鍵以繼續進行，並遵循所有其他提示。</span><span class="sxs-lookup"><span data-stu-id="03824-137">To set an administrative password for MySQL, press 'y' and then 'Enter' to continue, and follow any other prompts.</span></span> <span data-ttu-id="03824-138">此程序會安裝使用 PHP 搭配 MySQL 時所需的基本必要 PHP 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="03824-138">This process installs the minimum required PHP extensions needed to use PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="03824-139">請執行下列命令，以查看可以封裝形式提供的其他 PHP 擴充功能：</span><span class="sxs-lookup"><span data-stu-id="03824-139">Run the following command to see other PHP extensions that are available as packages:</span></span>

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a><span data-ttu-id="03824-140">建立 info.php 文件</span><span class="sxs-lookup"><span data-stu-id="03824-140">Create info.php document</span></span>
<span data-ttu-id="03824-141">您現在應可透過命令列輸入 `apache2 -v`、`mysql -v` 或 `php -v`，檢查您有哪個版本的 Apache、MySQL 和 PHP。</span><span class="sxs-lookup"><span data-stu-id="03824-141">You should now be able to check what version of Apache, MySQL, and PHP you have through the command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="03824-142">如果您想要進一步測試，您可以建立快速 PHP 資訊頁面，以在瀏覽器中檢視。</span><span class="sxs-lookup"><span data-stu-id="03824-142">If you would like to test further, you can create a quick PHP info page to view in a browser.</span></span> <span data-ttu-id="03824-143">透過以下命令，使用 Nano 文字編輯器建立檔案：</span><span class="sxs-lookup"><span data-stu-id="03824-143">Create a file with Nano text editor with this command:</span></span>

```bash
sudo nano /var/www/html/info.php
```

<span data-ttu-id="03824-144">在 GNU Nano 文字編輯器中，新增下列幾行：</span><span class="sxs-lookup"><span data-stu-id="03824-144">Within the GNU Nano text editor, add the following lines:</span></span>

```php
<?php
phpinfo();
?>
```

<span data-ttu-id="03824-145">然後，儲存並結束文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="03824-145">Then save and exit the text editor.</span></span>

<span data-ttu-id="03824-146">使用這個命令重新啟動 Apache，讓所有新的安裝生效。</span><span class="sxs-lookup"><span data-stu-id="03824-146">Restart Apache with this command so all new installs take effect.</span></span>

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="03824-147">確認 LAMP 安裝成功</span><span class="sxs-lookup"><span data-stu-id="03824-147">Verify LAMP successfully installed</span></span>
<span data-ttu-id="03824-148">現在您可以開啟瀏覽器並移至 http://youruniqueDNS/info.php，來檢查您建立的 PHP 資訊頁面。</span><span class="sxs-lookup"><span data-stu-id="03824-148">Now you can check the PHP info page you created by opening a browser and going to http://youruniqueDNS/info.php.</span></span> <span data-ttu-id="03824-149">該頁面看起來應該類似下圖。</span><span class="sxs-lookup"><span data-stu-id="03824-149">It should look similar to this image.</span></span>

![][2]

<span data-ttu-id="03824-150">前往 http://youruniqueDNS/ 檢視 Apache2 Ubuntu 預設頁面，即可檢查您的 Apache 安裝。</span><span class="sxs-lookup"><span data-stu-id="03824-150">You can check your Apache installation by viewing the Apache2 Ubuntu Default Page by going to you http://youruniqueDNS/.</span></span> <span data-ttu-id="03824-151">輸出類似於下列範例：</span><span class="sxs-lookup"><span data-stu-id="03824-151">The output is similar to the following example:</span></span>

![][3]

<span data-ttu-id="03824-152">恭喜，您剛已在 Azure VM 上安裝 LAMP 堆疊！</span><span class="sxs-lookup"><span data-stu-id="03824-152">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="03824-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="03824-153">Next steps</span></span>
<span data-ttu-id="03824-154">請查看 LAMP 堆疊上的 Ubuntu 文件︰</span><span class="sxs-lookup"><span data-stu-id="03824-154">Check out the Ubuntu documentation on the LAMP stack:</span></span>

* [<span data-ttu-id="03824-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="03824-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png
