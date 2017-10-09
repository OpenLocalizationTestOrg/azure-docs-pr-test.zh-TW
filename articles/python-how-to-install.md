---
title: "aaaInstall Python 和 hello SDK-Azure"
description: "深入了解如何使用 Azure tooinstall Python 和 hello SDK toouse。"
services: 
documentationcenter: python
author: lmazuel
manager: wpickett
editor: 
ms.assetid: f36294be-daeb-4caf-9129-fce18130f552
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 09/06/2016
ms.author: lmazuel
ms.openlocfilehash: c1b394770f9abd3e654a23d79ae179a9af89e2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="installing-python-and-hello-sdk"></a>安裝 Python 和 hello SDK
Python 輕鬆 tooset 由 Windows 和 Mac、 Linux、 上線預先安裝和[撞 for Windows](https://msdn.microsoft.com/commandline/wsl/about)。 本指南將逐步引導您完成安裝作業，並讓機器做好搭配 Azure 的準備。

## <a name="whats-in-hello-python-azure-sdk"></a>什麼是在 hello Python Azure SDK？
hello Azure SDK for Python 包含 toodevelop 可讓您的元件、 部署和管理 Azure 的 Python 應用程式。 具體來說，hello Azure SDK for Python 包含 hello 下列：

* **管理程式庫**。 這些類別庫提供一個可管理 Azure 資源 (例如儲存體帳戶、虛擬機器) 的介面。
* **執行階段程式庫**。 這些類別庫提供一個可存取 Azure 功能 (例如儲存體和服務匯流排) 的介面。

## <a name="which-python-and-which-version-toouse"></a>Python 和哪些版本 toouse
可用的 Python 解譯器有數種，範例包括：

* CPython-hello 標準和最常使用 Python 解譯器
* PyPy-快速且符合標準的替代實作 tooCPython
* IronPython - 可在 .Net/CLR 上執行的 Python 解譯器
* Jython-hello Java 虛擬機器執行的 Python 解譯器

**CPython** 2.7 版或 v3.3 + 和 PyPy 5.4.0 測試及支援 hello Python Azure SDK。

## <a name="where-tooget-python"></a>其中 tooget Python 嗎？
有數種方式 tooget CPython:

* 直接從 [www.python.org][www.python.org]
* 從聲譽良好的散發網站取得，如 [www.continuum.io][www.continuum.io]、[www.enthought.com][www.enthought.com] 或 [www.activestate.com][www.activestate.com]
* 從原始碼組建！

除非您有特定需要，我們建議 hello 前兩個選項。

## <a name="sdk-installation-on-windows-linux-and-macos-client-libraries-only"></a>Windows、Linux 及 MacOS 上的 SDK 安裝 (僅限用戶端程式庫)
如果您已經有安裝 Python，您可以使用 pip tooinstall 所有現有的 Python 2.7 或 Python 3.3 + 環境中的 hello 用戶端程式庫的組合。 這會下載 hello 封裝從 hello [Python 封裝索引][ Python Package Index] (PyPI)。

您可能需要系統管理員權限：

* Linux 及 MacOS，使用 hello`sudo`命令： `sudo pip install azure-mgmt-compute`。
* Windows：以系統管理員身分開啟 PowerShell/命令提示字元。

您可以為每個 Azure 服務個別安裝程式庫：

```console
   $ pip install azure-batch          # Install hello latest Batch runtime library
   $ pip install azure-mgmt-scheduler # Install hello latest Storage management library
```

預覽封裝都可以使用安裝 hello`--pre`旗標：

```console
   $ pip install --pre azure-mgmt-compute # installs only hello latest Compute Management library
```

您也可以安裝一組 Azure 程式庫在單行中輸入使用 hello`azure`中繼封裝。 此中繼套件中的並非所有封裝都尚未都發行為穩定，因為 hello`azure`中繼封裝仍處於預覽狀態。
不過，hello 核心封裝，從程式碼品質/完整性檢視方塊可視為 「 穩定 」 這一次

* 我們會儘快將它正式標示為穩定版以與其他語言一致。
  在那之前，我們不打算進行任何進一步的重大變更。

因為這是預覽版本，您需要 toouse hello`--pre`旗標：

```console
   $ pip install --pre azure
```

或直接使用

```console
   $ pip install azure==2.0.0rc6
```

## <a name="getting-more-packages"></a>取得更多封裝
hello [Python 封裝索引][ Python Package Index] (PyPI) 具有豐富的選取範圍的 Python 程式庫。  如果您選擇 tooinstall Distro，您已經將有大部分的 hello 有趣的各種案例，從 web 開發 tooTechnical 的位元運算。

## <a name="python-tools-for-visual-studio"></a>Python Tools for Visual Studio
[適用於 Visual Studio 的 Python 工具][適用於 Visual Studio 的 Python 工具] (PTVS) 是 Microsoft 提供的免費/OSS 外掛程式，它能將 VS 轉變為成熟的 Python IDE：

![how-to-install-python-ptvs](./media/python-how-to-install/how-to-install-python-ptvs.png)

您可以選擇是否要使用 PTVS，不過我們建議您使用，因為它能提供 Python 和 Web 專案/方案支援、偵錯、分析、互動式視窗、範本編輯和 IntelliSense。

PTVS 也很容易 toodeploy tooMicrosoft Azure 中，具備支援的部署太[雲端服務](cloud-services/cloud-services-python-ptvs.md)和[網站](app-service-web/web-sites-python-ptvs-django-mysql.md)。

PTVS 可以和您現有的 Visual Studio 2013、2015 或 2017 安裝一同運作。  如需文件、下載項目和相關討論，請參閱[適用於 Visual Studio 的 Python 工具]。  

## <a name="python-azure-scenarios-for-linux-and-macos"></a>適用於 Linux 和 MacOS 的 Python Azure 案例
就 Linux 或 MacOS 而言，支援的 Azure 案例包括：

1. 使用 Azure 服務使用 Python hello 用戶端程式庫
2. 在 Linux VM 上執行應用程式
3. 開發和發佈 tooAzure 網站使用 Git

hello 第一個案例可讓您利用 hello Azure PaaS 功能例如 tooauthor 豐富的 web 應用程式[blob 儲存體](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，[佇列儲存體](storage/queues/storage-python-how-to-use-queue-storage.md)，[資料表儲存體](cosmos-db/table-storage-how-to-use-python.md)透過 hello Azure REST Api Pythonic 包裝函式等。 這些 Web 應用程式在 Windows、Mac 和 Linux 上的運作方式相同。  您也可以從您的本機開發電腦或 Azure 上執行的 Linux VM，使用這些用戶端程式庫。

Hello VM 案例中，您只要啟動您的選擇 （Ubuntu、 CentOS、 Suse） 的 Linux VM，並執行/管理您喜歡哪一點。  例如，您可以執行[IPython] [ IPython] REPL/筆記本 Windows/Mac/Linux 電腦和您的瀏覽器 tooa Linux 或 Windows 多處理序執行中 VM hello IPython 引擎在 Azure 上的點上。

如需詳細資訊 tooset 設定 Linux VM，請參閱 hello[建立執行 Linux 之虛擬機器](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)教學課程。

使用 Git 部署，您可以開發 Python web 應用程式，並將它發行 tooan Azure 網站從任何作業系統。  當您儲存機制 tooAzure，它會自動建立虛擬環境和 pip 安裝所需的封裝。

如需有關開發和發佈 Azure 網站的詳細資訊，請參閱 hello 的教學課程[建立網站 Django](app-service-web/web-sites-python-create-deploy-django-app.md)，[建立網站 Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md)，和[建立網站酒瓶](app-service-web/web-sites-python-create-deploy-flask-app.md)。 如需更多有關使用任何 WSGI 相容架構的一般資訊，請參閱[在 Azure 網站上設定 Python](app-service-web/web-sites-python-configure.md)。

## <a name="additional-software-and-resources"></a>其他軟體和資源：
* [Azure SDK for Python ReadTheDocs](http://azure-sdk-for-python.readthedocs.io/en/latest/)
* [Azure SDK for Python GitHub](https://github.com/Azure/azure-sdk-for-python)
* [適用於 Python 的官方 Azure 範例](https://azure.microsoft.com/documentation/samples/?platform=python)
* [Continuum Analytics Python 發佈][Continuum Analytics Python Distribution]
* [Enthought Python 發佈][Enthought Python Distribution]
* [ActiveState Python 發佈][ActiveState Python Distribution]
* [SciPy - Scientific Python 程式庫套件][SciPy - A suite of Scientific Python libraries]
* [NumPy - Python 的數值程式庫][NumPy - A numerics library for Python]
* [Django 專案 - 成熟的 Web 架構/CMS][Django Project - A mature web framework/CMS]
* [IPython - 先進的 Python REPL/Notebook][IPython - an advanced REPL/Notebook for Python]
* [GitHub 上適用於 Visual Studio 的 Python 工具][Python Tools for Visual Studio on GitHub]
* [Python 開發人員中心](/develop/python/)

[Continuum Analytics Python Distribution]: http://continuum.io
[Enthought Python Distribution]: http://www.enthought.com
[ActiveState Python Distribution]: http://www.activestate.com
[www.python.org]: http://www.python.org
[www.continuum.io]: http://continuum.io
[www.enthought.com]: http://www.enthought.com
[www.activestate.com]: http://www.activestate.com
[SciPy - A suite of Scientific Python libraries]: http://www.scipy.org
[NumPy - A numerics library for Python]: http://www.numpy.org
[Django Project - A mature web framework/CMS]: http://www.djangoproject.com
[IPython - an advanced REPL/Notebook for Python]: http://ipython.org
[IPython]: http://ipython.org
[IPython Notebook on Azure]: virtual-machines-linux-jupyter-notebook.md
[Cloud Services]: cloud-services-python-ptvs.md
[Websites]: web-sites-python-ptvs-django-mysql.md
[適用於 Visual Studio 的 Python 工具]: http://aka.ms/ptvs
[Python Tools for Visual Studio on GitHub]: https://github.com/microsoft/ptvs
[Python Package Index]: http://pypi.python.org/pypi
[Microsoft Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?LinkId=254281
[Microsoft Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?LinkID=516990
[Setting up a Linux VM via hello Azure portal]: create-and-configure-opensuse-vm-in-portal.md
[How toouse hello Azure Command-Line Interface]: crossplat-cmd-tools.md
[Create a Virtual Machine Running Linux]: virtual-machines-linux-quick-create-cli.md
[Creating Websites with Django]: web-sites-python-create-deploy-django-app.md
[Creating Websites with Bottle]: web-sites-python-create-deploy-bottle-app.md
[Creating Websites with Flask]: web-sites-python-create-deploy-flask-app.md
[Configuring Python with Azure Websites]: web-sites-python-configure.md
[table storage]: storage-python-how-to-use-table-storage.md
[queue storage]: storage-python-how-to-use-queue-storage.md
[blob storage]:storage/blobs/storage-python-how-to-use-blob-storage.md
