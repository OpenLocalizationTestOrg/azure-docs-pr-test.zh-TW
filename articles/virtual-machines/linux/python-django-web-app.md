---
title: "在 Azure Linux VM 上搭配 Django 的 Python Web 應用程式 | Microsoft Docs"
description: "了解如何使用 Linux VM，在 Azure 中裝載以 Django 作為基礎的 Web 應用程式。"
services: virtual-machines-linux
documentationcenter: python
author: huguesv
manager: wpickett
editor: 
tags: azure-resource-manager
ms.assetid: 00ad4c2c-4316-4f9a-913f-f7f49b158db7
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 05/31/2017
ms.author: huvalo
ms.openlocfilehash: 6e2ab8c7da7496d0e2b567a4bdc9341adcf01552
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="django-hello-world-web-app-on-a-linux-vm"></a><span data-ttu-id="40bb0-103">Linux VM 上的 Django Hello World Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="40bb0-103">Django Hello World web app on a Linux VM</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="40bb0-104">Windows</span><span class="sxs-lookup"><span data-stu-id="40bb0-104">Windows</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [<span data-ttu-id="40bb0-105">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="40bb0-105">Mac/Linux</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

<span data-ttu-id="40bb0-106">本教學課程會示範如何在 Azure 虛擬機器中裝載 Linux 中以 Django 作為基礎的網站。</span><span class="sxs-lookup"><span data-stu-id="40bb0-106">This tutorial shows you how to host a Django-based website in Linux in Azure Virtual Machines.</span></span> <span data-ttu-id="40bb0-107">在教學課程中，我們假設沒有 Azure 的使用經驗。</span><span class="sxs-lookup"><span data-stu-id="40bb0-107">In the tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="40bb0-108">當您完成教學課程時，將可在雲端啟動並執行以 Django 作為基礎的應用程式。</span><span class="sxs-lookup"><span data-stu-id="40bb0-108">When you finish the tutorial, you can have a Django-based application up and running in the cloud.</span></span>

<span data-ttu-id="40bb0-109">了解如何：</span><span class="sxs-lookup"><span data-stu-id="40bb0-109">Learn how to:</span></span>

* <span data-ttu-id="40bb0-110">設定 Azure 虛擬機器以裝載 Django。</span><span class="sxs-lookup"><span data-stu-id="40bb0-110">Set up an Azure virtual machine to host Django.</span></span> <span data-ttu-id="40bb0-111">雖然本教學課程說明如何針對 **Linux** 執行這項操作，您也可以針對 Azure 中裝載的 Windows Server VM 執行相同操作。</span><span class="sxs-lookup"><span data-stu-id="40bb0-111">Although this tutorial explains how to do this for **Linux**, you can do the same for a Windows Server VM hosted in Azure.</span></span> 
* <span data-ttu-id="40bb0-112">在 Linux 中建立新的 Django 應用程式。</span><span class="sxs-lookup"><span data-stu-id="40bb0-112">Create a new Django application in Linux.</span></span>

<span data-ttu-id="40bb0-113">本教學課程會示範如何建立基本的 Hello World Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="40bb0-113">The tutorial shows you how to build a basic Hello World web application.</span></span> <span data-ttu-id="40bb0-114">該應用程式是裝載於 Azure 虛擬機器中。</span><span class="sxs-lookup"><span data-stu-id="40bb0-114">The application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="40bb0-115">下列螢幕擷取畫面會顯示完成的應用程式：</span><span class="sxs-lookup"><span data-stu-id="40bb0-115">The following screenshot shows the completed application:</span></span>

![瀏覽器視窗會顯示 Azure 中的 Hello World 頁面](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-to-host-django"></a><span data-ttu-id="40bb0-117">建立並設定 Azure 虛擬機器以裝載 Django</span><span class="sxs-lookup"><span data-stu-id="40bb0-117">Create and set up an Azure virtual machine to host Django</span></span>

1. <span data-ttu-id="40bb0-118">若要使用 Ubuntu Server 14.04 LTS 發佈來建立 Azure 虛擬機器，請參閱[在 Azure 入口網站中建立 Linux 虛擬機器](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="40bb0-118">To create an Azure virtual machine with the Ubuntu Server 14.04 LTS distribution, see [Create a Linux virtual machine in the Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="40bb0-119">您也可以選擇密碼驗證來取代使用 SSH 公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="40bb0-119">You also can choose password authentication instead of using an SSH public key.</span></span>
2. <span data-ttu-id="40bb0-120">若要編輯允許內送至通訊埠 80 的 HTTP 流量之網路安全性群組，請參閱[在 Azure 入口網站中建立網路安全性群組](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md)。</span><span class="sxs-lookup"><span data-stu-id="40bb0-120">To edit the network security group to allow incoming HTTP traffic to port 80, see [Create network security groups in the Azure portal](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>
3. <span data-ttu-id="40bb0-121">(選擇性) 根據預設，新的虛擬機器沒有完整網域名稱 (FQDN)。</span><span class="sxs-lookup"><span data-stu-id="40bb0-121">(Optional) By default, your new virtual machine doesn't have a fully qualified domain name (FQDN).</span></span>  <span data-ttu-id="40bb0-122">若要使用 FQDN 建立 VM，請參閱[在 Azure 入口網站建立適用於 Windows VM 的 FQDN](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="40bb0-122">To create a VM with an FQDN, see [Create an FQDN in the Azure portal for a Windows VM](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="40bb0-123">完成本教學課程不需要這個步驟。</span><span class="sxs-lookup"><span data-stu-id="40bb0-123">This step is not required for completing this tutorial.</span></span>

## <span data-ttu-id="40bb0-124"><a id="setup"> </a>設定開發環境</span><span class="sxs-lookup"><span data-stu-id="40bb0-124"><a id="setup"> </a>Set up the development environment</span></span>
> [!NOTE]
> <span data-ttu-id="40bb0-125">如果您需要安裝 Python 或想要使用用戶端程式庫，請參閱 [Python 安裝指南](../../python-how-to-install.md)。</span><span class="sxs-lookup"><span data-stu-id="40bb0-125">If you need to install Python or want to use the client libraries, see the [Python installation guide](../../python-how-to-install.md).</span></span>

<span data-ttu-id="40bb0-126">Ubuntu Linux VM 已預先安裝 Python 2.7，但它並未隨附 Apache 或 Django。</span><span class="sxs-lookup"><span data-stu-id="40bb0-126">The Ubuntu Linux VM has Python 2.7 preinstalled, but it doesn't come with Apache or Django.</span></span> <span data-ttu-id="40bb0-127">完成下列步驟可連線至您的 VM，並安裝 Apache 和 Django：</span><span class="sxs-lookup"><span data-stu-id="40bb0-127">Complete the following steps to connect to your VM and install Apache and Django:</span></span>

1. <span data-ttu-id="40bb0-128">開啟新的終端機視窗。</span><span class="sxs-lookup"><span data-stu-id="40bb0-128">Open a new Terminal window.</span></span>
2. <span data-ttu-id="40bb0-129">若要連線至 Azure VM，請輸入下列命令。</span><span class="sxs-lookup"><span data-stu-id="40bb0-129">To connect to the Azure VM, enter the following command.</span></span> <span data-ttu-id="40bb0-130">如果您尚未建立 FQDN，您可以使用 Azure 入口網站之虛擬機器摘要所顯示的公用 IP 位址來進行連線。</span><span class="sxs-lookup"><span data-stu-id="40bb0-130">If you didn't create an FQDN, you can connect by using the public IP address that's displayed in the virtual machine summary in the Azure portal.</span></span>
   
       $ ssh yourusername@yourVmUrl
3. <span data-ttu-id="40bb0-131">若要安裝 Django，請輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="40bb0-131">To install Django, enter the following commands:</span></span>
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. <span data-ttu-id="40bb0-132">若要安裝含 mod-wsgi 的 Apache，請輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="40bb0-132">To install Apache with mod-wsgi, enter the following command:</span></span>
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a><span data-ttu-id="40bb0-133">建立新的 Django 應用程式</span><span class="sxs-lookup"><span data-stu-id="40bb0-133">Create a new Django app</span></span>
1. <span data-ttu-id="40bb0-134">若要使用 SSH 存取您的 VM，請開啟您在上一節中使用的終端機視窗。</span><span class="sxs-lookup"><span data-stu-id="40bb0-134">To use SSH to access your VM, open the Terminal window you used in the preceding section.</span></span>
2. <span data-ttu-id="40bb0-135">若要建立新的 Django 專案，請輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="40bb0-135">To create a new Django project, enter the following commands:</span></span>
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   <span data-ttu-id="40bb0-136">`django-admin.py` 指令碼會為以 Django 作為基礎的網站產生一個基本結構：</span><span class="sxs-lookup"><span data-stu-id="40bb0-136">The `django-admin.py` script generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="40bb0-137">`helloworld/manage.py` 可協助您開始裝載及停止裝載以 Django 作為基礎的網站。</span><span class="sxs-lookup"><span data-stu-id="40bb0-137">`helloworld/manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="40bb0-138">`helloworld/helloworld/settings.py` 具有您應用程式的 Django 設定。</span><span class="sxs-lookup"><span data-stu-id="40bb0-138">`helloworld/helloworld/settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="40bb0-139">`helloworld/helloworld/urls.py` 具有每個 URL 及其檢視之間的對應程式碼。</span><span class="sxs-lookup"><span data-stu-id="40bb0-139">`helloworld/helloworld/urls.py` has the mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="40bb0-140">在 /var/www/helloworld/helloworld 目錄中，建立名為 views.py 的新檔案。</span><span class="sxs-lookup"><span data-stu-id="40bb0-140">In the /var/www/helloworld/helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="40bb0-141">這個檔案具有轉譯 "hello world" 頁面的檢視。</span><span class="sxs-lookup"><span data-stu-id="40bb0-141">This file has the view that renders the "hello world" page.</span></span> <span data-ttu-id="40bb0-142">在程式碼編輯器中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="40bb0-142">In your code editor, enter the following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="40bb0-143">使用下列命令取代 urls.py 檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="40bb0-143">Replace the contents of the urls.py file with the following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a><span data-ttu-id="40bb0-144">設定 Apache</span><span class="sxs-lookup"><span data-stu-id="40bb0-144">Set up Apache</span></span>
1. <span data-ttu-id="40bb0-145">在 /etc/apache2/sites-available/helloworld.conf 資料夾中，建立 Apache 虛擬主機組態檔。</span><span class="sxs-lookup"><span data-stu-id="40bb0-145">In the /etc/apache2/sites-available/helloworld.conf folder, create an Apache virtual host configuration file.</span></span> <span data-ttu-id="40bb0-146">將內容設為下列值。</span><span class="sxs-lookup"><span data-stu-id="40bb0-146">Set the contents to the following values.</span></span> <span data-ttu-id="40bb0-147">以您所使用之電腦的實際名稱取代 yourVmName(例如 pyubuntu)。</span><span class="sxs-lookup"><span data-stu-id="40bb0-147">Replace *yourVmName* with the actual name of the machine you are using (for example, *pyubuntu*).</span></span>
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. <span data-ttu-id="40bb0-148">若要啟動站台，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="40bb0-148">To activate the site, use the following command:</span></span>
   
       $ sudo a2ensite helloworld
3. <span data-ttu-id="40bb0-149">若要重新啟動 Apache，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="40bb0-149">To restart Apache, use the following command:</span></span>
   
       $ sudo service apache2 reload
4. <span data-ttu-id="40bb0-150">在您的瀏覽器中載入網頁：</span><span class="sxs-lookup"><span data-stu-id="40bb0-150">Load the webpage in your browser:</span></span>
   
   ![瀏覽器視窗會顯示 Azure 中的 Hello World 頁面](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="40bb0-152">關閉 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="40bb0-152">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="40bb0-153">當您完成本教學課程時，建議您將為本教學課程建立的 Azure VM 關閉或移除。</span><span class="sxs-lookup"><span data-stu-id="40bb0-153">When you're done with this tutorial, we recommend that you shut down or remove the Azure VM you created for the tutorial.</span></span> <span data-ttu-id="40bb0-154">這樣可為其他教學課程釋放資源，您也可以避免產生 Azure 使用量費用。</span><span class="sxs-lookup"><span data-stu-id="40bb0-154">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

