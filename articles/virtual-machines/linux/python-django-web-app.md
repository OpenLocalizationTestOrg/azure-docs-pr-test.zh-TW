---
title: "aaaPython Django Azure Linux VM 上的 web 應用程式 |Microsoft 文件"
description: "了解如何 toohost Django 為基礎的 web 應用程式使用 Linux VM 在 Azure 中。"
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
ms.openlocfilehash: 520c47e19e8ffb4bb866f70772d506ddf76e242c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="django-hello-world-web-app-on-a-linux-vm"></a><span data-ttu-id="7a4c9-103">Linux VM 上的 Django Hello World Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7a4c9-103">Django Hello World web app on a Linux VM</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7a4c9-104">Windows</span><span class="sxs-lookup"><span data-stu-id="7a4c9-104">Windows</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [<span data-ttu-id="7a4c9-105">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="7a4c9-105">Mac/Linux</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

<span data-ttu-id="7a4c9-106">本教學課程示範如何 toohost Django 架構網站在 Azure 虛擬機器中的 Linux。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-106">This tutorial shows you how toohost a Django-based website in Linux in Azure Virtual Machines.</span></span> <span data-ttu-id="7a4c9-107">在 hello 教學課程中，我們會假設沒有與 Azure 的使用經驗。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-107">In hello tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="7a4c9-108">當您完成 hello 教學課程時，您可以如 Django 架構應用程式註冊以及 hello 雲端中執行。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-108">When you finish hello tutorial, you can have a Django-based application up and running in hello cloud.</span></span>

<span data-ttu-id="7a4c9-109">了解如何：</span><span class="sxs-lookup"><span data-stu-id="7a4c9-109">Learn how to:</span></span>

* <span data-ttu-id="7a4c9-110">設定 Azure 虛擬機器 toohost Django。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-110">Set up an Azure virtual machine toohost Django.</span></span> <span data-ttu-id="7a4c9-111">雖然本教學課程說明如何 toodo 此作業對於**Linux**，您可以相同 hello Azure 中裝載 Windows Server VM。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-111">Although this tutorial explains how toodo this for **Linux**, you can do hello same for a Windows Server VM hosted in Azure.</span></span> 
* <span data-ttu-id="7a4c9-112">在 Linux 中建立新的 Django 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-112">Create a new Django application in Linux.</span></span>

<span data-ttu-id="7a4c9-113">hello 教學課程會示範如何 toobuild 基本的 Hello World web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-113">hello tutorial shows you how toobuild a basic Hello World web application.</span></span> <span data-ttu-id="7a4c9-114">hello 應用程式裝載於 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-114">hello application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="7a4c9-115">下列螢幕擷取畫面的 hello 顯示 hello 完成應用程式：</span><span class="sxs-lookup"><span data-stu-id="7a4c9-115">hello following screenshot shows hello completed application:</span></span>

![瀏覽器視窗會顯示在 Azure 中的 hello Hello World 網頁](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a><span data-ttu-id="7a4c9-117">建立並設定 Azure 虛擬機器 toohost Django</span><span class="sxs-lookup"><span data-stu-id="7a4c9-117">Create and set up an Azure virtual machine toohost Django</span></span>

1. <span data-ttu-id="7a4c9-118">toocreate Azure 虛擬機器以 hello Ubuntu Server 14.04 LTS 分佈，請參閱[hello Azure 入口網站中建立 Linux 虛擬機器](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-118">toocreate an Azure virtual machine with hello Ubuntu Server 14.04 LTS distribution, see [Create a Linux virtual machine in hello Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="7a4c9-119">您也可以選擇密碼驗證來取代使用 SSH 公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-119">You also can choose password authentication instead of using an SSH public key.</span></span>
2. <span data-ttu-id="7a4c9-120">tooedit hello 網路安全性群組 tooallow 連入 HTTP 流量 tooport 80，請參閱[hello Azure 入口網站中建立網路安全性群組](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md)。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-120">tooedit hello network security group tooallow incoming HTTP traffic tooport 80, see [Create network security groups in hello Azure portal](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>
3. <span data-ttu-id="7a4c9-121">(選擇性) 根據預設，新的虛擬機器沒有完整網域名稱 (FQDN)。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-121">(Optional) By default, your new virtual machine doesn't have a fully qualified domain name (FQDN).</span></span>  <span data-ttu-id="7a4c9-122">toocreate VM 使用 FQDN，請參閱[hello Azure 入口網站中建立的 FQDN，針對 Windows VM](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-122">toocreate a VM with an FQDN, see [Create an FQDN in hello Azure portal for a Windows VM](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="7a4c9-123">完成本教學課程不需要這個步驟。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-123">This step is not required for completing this tutorial.</span></span>

## <span data-ttu-id="7a4c9-124"><a id="setup"></a>設定 hello 開發環境</span><span class="sxs-lookup"><span data-stu-id="7a4c9-124"><a id="setup"> </a>Set up hello development environment</span></span>
> [!NOTE]
> <span data-ttu-id="7a4c9-125">如果您需要 tooinstall Python，或想 toouse hello 用戶端程式庫，請參閱 hello [Python 安裝指南](../../python-how-to-install.md)。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-125">If you need tooinstall Python or want toouse hello client libraries, see hello [Python installation guide](../../python-how-to-install.md).</span></span>

<span data-ttu-id="7a4c9-126">hello Ubuntu Linux VM Python 2.7 預先安裝，但它並未隨附 Apache 或 Django。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-126">hello Ubuntu Linux VM has Python 2.7 preinstalled, but it doesn't come with Apache or Django.</span></span> <span data-ttu-id="7a4c9-127">完成下列步驟 tooconnect tooyour VM hello 和安裝 Apache 和 Django:</span><span class="sxs-lookup"><span data-stu-id="7a4c9-127">Complete hello following steps tooconnect tooyour VM and install Apache and Django:</span></span>

1. <span data-ttu-id="7a4c9-128">開啟新的終端機視窗。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-128">Open a new Terminal window.</span></span>
2. <span data-ttu-id="7a4c9-129">tooconnect toohello Azure VM 中，輸入下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-129">tooconnect toohello Azure VM, enter hello following command.</span></span> <span data-ttu-id="7a4c9-130">如果您未建立的 FQDN，您可以使用 hello 公用 IP 位址，會顯示在摘要 hello Azure 入口網站中的 hello 虛擬機器進行連接。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-130">If you didn't create an FQDN, you can connect by using hello public IP address that's displayed in hello virtual machine summary in hello Azure portal.</span></span>
   
       $ ssh yourusername@yourVmUrl
3. <span data-ttu-id="7a4c9-131">tooinstall Django，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="7a4c9-131">tooinstall Django, enter hello following commands:</span></span>
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. <span data-ttu-id="7a4c9-132">tooinstall Apache 與 mod wsgi，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="7a4c9-132">tooinstall Apache with mod-wsgi, enter hello following command:</span></span>
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a><span data-ttu-id="7a4c9-133">建立新的 Django 應用程式</span><span class="sxs-lookup"><span data-stu-id="7a4c9-133">Create a new Django app</span></span>
1. <span data-ttu-id="7a4c9-134">toouse SSH tooaccess hello 前面一節中使用您的 VM、 開啟 hello 終端機視窗。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-134">toouse SSH tooaccess your VM, open hello Terminal window you used in hello preceding section.</span></span>
2. <span data-ttu-id="7a4c9-135">toocreate 新 Django 專案中，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="7a4c9-135">toocreate a new Django project, enter hello following commands:</span></span>
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   <span data-ttu-id="7a4c9-136">hello`django-admin.py`指令碼會產生如 Django 架構網站的基本結構：</span><span class="sxs-lookup"><span data-stu-id="7a4c9-136">hello `django-admin.py` script generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="7a4c9-137">`helloworld/manage.py` 可協助您開始裝載及停止裝載以 Django 作為基礎的網站。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-137">`helloworld/manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="7a4c9-138">`helloworld/helloworld/settings.py` 具有您應用程式的 Django 設定。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-138">`helloworld/helloworld/settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="7a4c9-139">`helloworld/helloworld/urls.py`具有 hello 每個 URL 和它的檢視之間的對應程式碼。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-139">`helloworld/helloworld/urls.py` has hello mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="7a4c9-140">在 hello /var/www/helloworld/helloworld 目錄中，建立名為 views.py 新檔案。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-140">In hello /var/www/helloworld/helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="7a4c9-141">此檔案具有 hello 檢視呈現 hello"hello world"的頁面。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-141">This file has hello view that renders hello "hello world" page.</span></span> <span data-ttu-id="7a4c9-142">在程式碼編輯器中，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="7a4c9-142">In your code editor, enter hello following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="7a4c9-143">取代下列命令的 hello hello hello urls.py 檔案內容：</span><span class="sxs-lookup"><span data-stu-id="7a4c9-143">Replace hello contents of hello urls.py file with hello following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a><span data-ttu-id="7a4c9-144">設定 Apache</span><span class="sxs-lookup"><span data-stu-id="7a4c9-144">Set up Apache</span></span>
1. <span data-ttu-id="7a4c9-145">在 hello /etc/apache2/sites-available/helloworld.conf 資料夾中建立的 Apache 虛擬主機設定檔。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-145">In hello /etc/apache2/sites-available/helloworld.conf folder, create an Apache virtual host configuration file.</span></span> <span data-ttu-id="7a4c9-146">設定下列值的 hello 內容 toohello。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-146">Set hello contents toohello following values.</span></span> <span data-ttu-id="7a4c9-147">取代*yourVmName* hello 的 hello 機器您要使用的實際名稱 (例如， *pyubuntu*)。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-147">Replace *yourVmName* with hello actual name of hello machine you are using (for example, *pyubuntu*).</span></span>
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. <span data-ttu-id="7a4c9-148">下列命令使用 hello tooactivate hello 網站：</span><span class="sxs-lookup"><span data-stu-id="7a4c9-148">tooactivate hello site, use hello following command:</span></span>
   
       $ sudo a2ensite helloworld
3. <span data-ttu-id="7a4c9-149">toorestart Apache，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="7a4c9-149">toorestart Apache, use hello following command:</span></span>
   
       $ sudo service apache2 reload
4. <span data-ttu-id="7a4c9-150">載入 hello 網頁瀏覽器中：</span><span class="sxs-lookup"><span data-stu-id="7a4c9-150">Load hello webpage in your browser:</span></span>
   
   ![在瀏覽器視窗會顯示在 Azure 中的 hello hello world 網頁](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="7a4c9-152">關閉 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="7a4c9-152">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="7a4c9-153">當您完成本教學課程中時，我們建議您關閉或移除 hello hello 教學課程中建立的 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-153">When you're done with this tutorial, we recommend that you shut down or remove hello Azure VM you created for hello tutorial.</span></span> <span data-ttu-id="7a4c9-154">這樣可為其他教學課程釋放資源，您也可以避免產生 Azure 使用量費用。</span><span class="sxs-lookup"><span data-stu-id="7a4c9-154">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

