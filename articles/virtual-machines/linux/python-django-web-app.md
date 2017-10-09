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
# <a name="django-hello-world-web-app-on-a-linux-vm"></a>Linux VM 上的 Django Hello World Web 應用程式
> [!div class="op_single_selector"]
> * [Windows](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [Mac/Linux](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

本教學課程示範如何 toohost Django 架構網站在 Azure 虛擬機器中的 Linux。 在 hello 教學課程中，我們會假設沒有與 Azure 的使用經驗。 當您完成 hello 教學課程時，您可以如 Django 架構應用程式註冊以及 hello 雲端中執行。

了解如何：

* 設定 Azure 虛擬機器 toohost Django。 雖然本教學課程說明如何 toodo 此作業對於**Linux**，您可以相同 hello Azure 中裝載 Windows Server VM。 
* 在 Linux 中建立新的 Django 應用程式。

hello 教學課程會示範如何 toobuild 基本的 Hello World web 應用程式。 hello 應用程式裝載於 Azure 虛擬機器。

下列螢幕擷取畫面的 hello 顯示 hello 完成應用程式：

![瀏覽器視窗會顯示在 Azure 中的 hello Hello World 網頁](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a>建立並設定 Azure 虛擬機器 toohost Django

1. toocreate Azure 虛擬機器以 hello Ubuntu Server 14.04 LTS 分佈，請參閱[hello Azure 入口網站中建立 Linux 虛擬機器](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 您也可以選擇密碼驗證來取代使用 SSH 公開金鑰。
2. tooedit hello 網路安全性群組 tooallow 連入 HTTP 流量 tooport 80，請參閱[hello Azure 入口網站中建立網路安全性群組](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md)。
3. (選擇性) 根據預設，新的虛擬機器沒有完整網域名稱 (FQDN)。  toocreate VM 使用 FQDN，請參閱[hello Azure 入口網站中建立的 FQDN，針對 Windows VM](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 完成本教學課程不需要這個步驟。

## <a id="setup"></a>設定 hello 開發環境
> [!NOTE]
> 如果您需要 tooinstall Python，或想 toouse hello 用戶端程式庫，請參閱 hello [Python 安裝指南](../../python-how-to-install.md)。

hello Ubuntu Linux VM Python 2.7 預先安裝，但它並未隨附 Apache 或 Django。 完成下列步驟 tooconnect tooyour VM hello 和安裝 Apache 和 Django:

1. 開啟新的終端機視窗。
2. tooconnect toohello Azure VM 中，輸入下列命令的 hello。 如果您未建立的 FQDN，您可以使用 hello 公用 IP 位址，會顯示在摘要 hello Azure 入口網站中的 hello 虛擬機器進行連接。
   
       $ ssh yourusername@yourVmUrl
3. tooinstall Django，輸入下列命令的 hello:
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. tooinstall Apache 與 mod wsgi，輸入下列命令的 hello:
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a>建立新的 Django 應用程式
1. toouse SSH tooaccess hello 前面一節中使用您的 VM、 開啟 hello 終端機視窗。
2. toocreate 新 Django 專案中，輸入下列命令的 hello:
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   hello`django-admin.py`指令碼會產生如 Django 架構網站的基本結構：
   
   * `helloworld/manage.py` 可協助您開始裝載及停止裝載以 Django 作為基礎的網站。
   * `helloworld/helloworld/settings.py` 具有您應用程式的 Django 設定。
   * `helloworld/helloworld/urls.py`具有 hello 每個 URL 和它的檢視之間的對應程式碼。
3. 在 hello /var/www/helloworld/helloworld 目錄中，建立名為 views.py 新檔案。 此檔案具有 hello 檢視呈現 hello"hello world"的頁面。 在程式碼編輯器中，輸入下列命令的 hello:
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. 取代下列命令的 hello hello hello urls.py 檔案內容：
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a>設定 Apache
1. 在 hello /etc/apache2/sites-available/helloworld.conf 資料夾中建立的 Apache 虛擬主機設定檔。 設定下列值的 hello 內容 toohello。 取代*yourVmName* hello 的 hello 機器您要使用的實際名稱 (例如， *pyubuntu*)。
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. 下列命令使用 hello tooactivate hello 網站：
   
       $ sudo a2ensite helloworld
3. toorestart Apache，使用下列命令的 hello:
   
       $ sudo service apache2 reload
4. 載入 hello 網頁瀏覽器中：
   
   ![在瀏覽器視窗會顯示在 Azure 中的 hello hello world 網頁](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a>關閉 Azure 虛擬機器
當您完成本教學課程中時，我們建議您關閉或移除 hello hello 教學課程中建立的 Azure VM。 這樣可為其他教學課程釋放資源，您也可以避免產生 Azure 使用量費用。

