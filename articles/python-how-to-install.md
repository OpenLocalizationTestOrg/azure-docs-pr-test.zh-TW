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
# <a name="installing-python-and-hello-sdk"></a><span data-ttu-id="fe22e-103">安裝 Python 和 hello SDK</span><span class="sxs-lookup"><span data-stu-id="fe22e-103">Installing Python and hello SDK</span></span>
<span data-ttu-id="fe22e-104">Python 輕鬆 tooset 由 Windows 和 Mac、 Linux、 上線預先安裝和[撞 for Windows](https://msdn.microsoft.com/commandline/wsl/about)。</span><span class="sxs-lookup"><span data-stu-id="fe22e-104">Python is easy tooset up on Windows and comes pre-installed on Mac, Linux, and [Bash for Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span> <span data-ttu-id="fe22e-105">本指南將逐步引導您完成安裝作業，並讓機器做好搭配 Azure 的準備。</span><span class="sxs-lookup"><span data-stu-id="fe22e-105">This guide walks you through installation and getting your machine ready for use with Azure.</span></span>

## <a name="whats-in-hello-python-azure-sdk"></a><span data-ttu-id="fe22e-106">什麼是在 hello Python Azure SDK？</span><span class="sxs-lookup"><span data-stu-id="fe22e-106">What's in hello Python Azure SDK?</span></span>
<span data-ttu-id="fe22e-107">hello Azure SDK for Python 包含 toodevelop 可讓您的元件、 部署和管理 Azure 的 Python 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fe22e-107">hello Azure SDK for Python includes components that allow you toodevelop, deploy, and manage Python applications for Azure.</span></span> <span data-ttu-id="fe22e-108">具體來說，hello Azure SDK for Python 包含 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="fe22e-108">Specifically, hello Azure SDK for Python includes hello following:</span></span>

* <span data-ttu-id="fe22e-109">**管理程式庫**。</span><span class="sxs-lookup"><span data-stu-id="fe22e-109">**Management libraries**.</span></span> <span data-ttu-id="fe22e-110">這些類別庫提供一個可管理 Azure 資源 (例如儲存體帳戶、虛擬機器) 的介面。</span><span class="sxs-lookup"><span data-stu-id="fe22e-110">These class libraries provide an interface managing Azure resources, such as storage accounts, virtual machines.</span></span>
* <span data-ttu-id="fe22e-111">**執行階段程式庫**。</span><span class="sxs-lookup"><span data-stu-id="fe22e-111">**Runtime libraries**.</span></span> <span data-ttu-id="fe22e-112">這些類別庫提供一個可存取 Azure 功能 (例如儲存體和服務匯流排) 的介面。</span><span class="sxs-lookup"><span data-stu-id="fe22e-112">These class libraries provide an interface for accessing Azure features, such as storage and service bus.</span></span>

## <a name="which-python-and-which-version-toouse"></a><span data-ttu-id="fe22e-113">Python 和哪些版本 toouse</span><span class="sxs-lookup"><span data-stu-id="fe22e-113">Which Python and which version toouse</span></span>
<span data-ttu-id="fe22e-114">可用的 Python 解譯器有數種，範例包括：</span><span class="sxs-lookup"><span data-stu-id="fe22e-114">There are several flavors of Python interpreters available - examples include:</span></span>

* <span data-ttu-id="fe22e-115">CPython-hello 標準和最常使用 Python 解譯器</span><span class="sxs-lookup"><span data-stu-id="fe22e-115">CPython - hello standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="fe22e-116">PyPy-快速且符合標準的替代實作 tooCPython</span><span class="sxs-lookup"><span data-stu-id="fe22e-116">PyPy - fast, compliant alternative implementation tooCPython</span></span>
* <span data-ttu-id="fe22e-117">IronPython - 可在 .Net/CLR 上執行的 Python 解譯器</span><span class="sxs-lookup"><span data-stu-id="fe22e-117">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="fe22e-118">Jython-hello Java 虛擬機器執行的 Python 解譯器</span><span class="sxs-lookup"><span data-stu-id="fe22e-118">Jython - Python interpreter that runs on hello Java Virtual Machine</span></span>

<span data-ttu-id="fe22e-119">**CPython** 2.7 版或 v3.3 + 和 PyPy 5.4.0 測試及支援 hello Python Azure SDK。</span><span class="sxs-lookup"><span data-stu-id="fe22e-119">**CPython** v2.7 or v3.3+ and PyPy 5.4.0 are tested and supported for hello Python Azure SDK.</span></span>

## <a name="where-tooget-python"></a><span data-ttu-id="fe22e-120">其中 tooget Python 嗎？</span><span class="sxs-lookup"><span data-stu-id="fe22e-120">Where tooget Python?</span></span>
<span data-ttu-id="fe22e-121">有數種方式 tooget CPython:</span><span class="sxs-lookup"><span data-stu-id="fe22e-121">There are several ways tooget CPython:</span></span>

* <span data-ttu-id="fe22e-122">直接從 [www.python.org][www.python.org]</span><span class="sxs-lookup"><span data-stu-id="fe22e-122">Directly from [www.python.org][www.python.org]</span></span>
* <span data-ttu-id="fe22e-123">從聲譽良好的散發網站取得，如 [www.continuum.io][www.continuum.io]、[www.enthought.com][www.enthought.com] 或 [www.activestate.com][www.activestate.com]</span><span class="sxs-lookup"><span data-stu-id="fe22e-123">From a reputable distro such as [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] or [www.activestate.com][www.activestate.com]</span></span>
* <span data-ttu-id="fe22e-124">從原始碼組建！</span><span class="sxs-lookup"><span data-stu-id="fe22e-124">Build from source!</span></span>

<span data-ttu-id="fe22e-125">除非您有特定需要，我們建議 hello 前兩個選項。</span><span class="sxs-lookup"><span data-stu-id="fe22e-125">Unless you have a specific need, we recommend hello first two options.</span></span>

## <a name="sdk-installation-on-windows-linux-and-macos-client-libraries-only"></a><span data-ttu-id="fe22e-126">Windows、Linux 及 MacOS 上的 SDK 安裝 (僅限用戶端程式庫)</span><span class="sxs-lookup"><span data-stu-id="fe22e-126">SDK Installation on Windows, Linux, and MacOS (client libraries only)</span></span>
<span data-ttu-id="fe22e-127">如果您已經有安裝 Python，您可以使用 pip tooinstall 所有現有的 Python 2.7 或 Python 3.3 + 環境中的 hello 用戶端程式庫的組合。</span><span class="sxs-lookup"><span data-stu-id="fe22e-127">If you already have Python installed, you can use pip tooinstall a bundle of all hello client libraries in your existing Python 2.7 or Python 3.3+ environment.</span></span> <span data-ttu-id="fe22e-128">這會下載 hello 封裝從 hello [Python 封裝索引][ Python Package Index] (PyPI)。</span><span class="sxs-lookup"><span data-stu-id="fe22e-128">This downloads hello packages from hello [Python Package Index][Python Package Index] (PyPI).</span></span>

<span data-ttu-id="fe22e-129">您可能需要系統管理員權限：</span><span class="sxs-lookup"><span data-stu-id="fe22e-129">You may need administrator rights:</span></span>

* <span data-ttu-id="fe22e-130">Linux 及 MacOS，使用 hello`sudo`命令： `sudo pip install azure-mgmt-compute`。</span><span class="sxs-lookup"><span data-stu-id="fe22e-130">Linux and MacOS, use hello `sudo` command: `sudo pip install azure-mgmt-compute`.</span></span>
* <span data-ttu-id="fe22e-131">Windows：以系統管理員身分開啟 PowerShell/命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="fe22e-131">Windows: open your PowerShell/Command prompt as an administrator</span></span>

<span data-ttu-id="fe22e-132">您可以為每個 Azure 服務個別安裝程式庫：</span><span class="sxs-lookup"><span data-stu-id="fe22e-132">You can install individually each library for each Azure service:</span></span>

```console
   $ pip install azure-batch          # Install hello latest Batch runtime library
   $ pip install azure-mgmt-scheduler # Install hello latest Storage management library
```

<span data-ttu-id="fe22e-133">預覽封裝都可以使用安裝 hello`--pre`旗標：</span><span class="sxs-lookup"><span data-stu-id="fe22e-133">Preview packages can be installed using hello `--pre` flag:</span></span>

```console
   $ pip install --pre azure-mgmt-compute # installs only hello latest Compute Management library
```

<span data-ttu-id="fe22e-134">您也可以安裝一組 Azure 程式庫在單行中輸入使用 hello`azure`中繼封裝。</span><span class="sxs-lookup"><span data-stu-id="fe22e-134">You can also install a set of Azure libraries in a single line using hello `azure` meta-package.</span></span> <span data-ttu-id="fe22e-135">此中繼套件中的並非所有封裝都尚未都發行為穩定，因為 hello`azure`中繼封裝仍處於預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="fe22e-135">Since not all packages in this meta-package are published as stable yet, hello `azure` meta-package is still in preview.</span></span>
<span data-ttu-id="fe22e-136">不過，hello 核心封裝，從程式碼品質/完整性檢視方塊可視為 「 穩定 」 這一次</span><span class="sxs-lookup"><span data-stu-id="fe22e-136">However, hello core packages, from code quality/completeness perspectives can be considered "stable" at this time</span></span>

* <span data-ttu-id="fe22e-137">我們會儘快將它正式標示為穩定版以與其他語言一致。</span><span class="sxs-lookup"><span data-stu-id="fe22e-137">it is officially labeled as such in sync with other languages as soon as possible.</span></span>
  <span data-ttu-id="fe22e-138">在那之前，我們不打算進行任何進一步的重大變更。</span><span class="sxs-lookup"><span data-stu-id="fe22e-138">We are not planning on any further major changes until then.</span></span>

<span data-ttu-id="fe22e-139">因為這是預覽版本，您需要 toouse hello`--pre`旗標：</span><span class="sxs-lookup"><span data-stu-id="fe22e-139">Since it's a preview release, you need toouse hello `--pre` flag:</span></span>

```console
   $ pip install --pre azure
```

<span data-ttu-id="fe22e-140">或直接使用</span><span class="sxs-lookup"><span data-stu-id="fe22e-140">or directly</span></span>

```console
   $ pip install azure==2.0.0rc6
```

## <a name="getting-more-packages"></a><span data-ttu-id="fe22e-141">取得更多封裝</span><span class="sxs-lookup"><span data-stu-id="fe22e-141">Getting More Packages</span></span>
<span data-ttu-id="fe22e-142">hello [Python 封裝索引][ Python Package Index] (PyPI) 具有豐富的選取範圍的 Python 程式庫。</span><span class="sxs-lookup"><span data-stu-id="fe22e-142">hello [Python Package Index][Python Package Index] (PyPI) has a rich selection of Python libraries.</span></span>  <span data-ttu-id="fe22e-143">如果您選擇 tooinstall Distro，您已經將有大部分的 hello 有趣的各種案例，從 web 開發 tooTechnical 的位元運算。</span><span class="sxs-lookup"><span data-stu-id="fe22e-143">If you chose tooinstall a Distro, you'll already have most of hello interesting bits for various scenarios from web development tooTechnical Computing.</span></span>

## <a name="python-tools-for-visual-studio"></a><span data-ttu-id="fe22e-144">Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fe22e-144">Python Tools for Visual Studio</span></span>
<span data-ttu-id="fe22e-145">[適用於 Visual Studio 的 Python 工具][適用於 Visual Studio 的 Python 工具] (PTVS) 是 Microsoft 提供的免費/OSS 外掛程式，它能將 VS 轉變為成熟的 Python IDE：</span><span class="sxs-lookup"><span data-stu-id="fe22e-145">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) is a free/OSS plugin from Microsoft, which turns VS into a full-fledged Python IDE:</span></span>

![how-to-install-python-ptvs](./media/python-how-to-install/how-to-install-python-ptvs.png)

<span data-ttu-id="fe22e-147">您可以選擇是否要使用 PTVS，不過我們建議您使用，因為它能提供 Python 和 Web 專案/方案支援、偵錯、分析、互動式視窗、範本編輯和 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="fe22e-147">Using PTVS is optional, but is recommended as it gives you Python and Web Project/Solution support, debugging, profiling, interactive window, Template editing, and Intellisense.</span></span>

<span data-ttu-id="fe22e-148">PTVS 也很容易 toodeploy tooMicrosoft Azure 中，具備支援的部署太[雲端服務](cloud-services/cloud-services-python-ptvs.md)和[網站](app-service-web/web-sites-python-ptvs-django-mysql.md)。</span><span class="sxs-lookup"><span data-stu-id="fe22e-148">PTVS also makes it easy toodeploy tooMicrosoft Azure, with support for deployment too[Cloud Services](cloud-services/cloud-services-python-ptvs.md) and [Websites](app-service-web/web-sites-python-ptvs-django-mysql.md).</span></span>

<span data-ttu-id="fe22e-149">PTVS 可以和您現有的 Visual Studio 2013、2015 或 2017 安裝一同運作。</span><span class="sxs-lookup"><span data-stu-id="fe22e-149">PTVS works with your existing Visual Studio 2013, 2015, or 2017 installation.</span></span>  <span data-ttu-id="fe22e-150">如需文件、下載項目和相關討論，請參閱[適用於 Visual Studio 的 Python 工具]。</span><span class="sxs-lookup"><span data-stu-id="fe22e-150">For documentation, downloads and discussions, see [Python Tools for Visual Studio].</span></span>  

## <a name="python-azure-scenarios-for-linux-and-macos"></a><span data-ttu-id="fe22e-151">適用於 Linux 和 MacOS 的 Python Azure 案例</span><span class="sxs-lookup"><span data-stu-id="fe22e-151">Python Azure Scenarios for Linux and MacOS</span></span>
<span data-ttu-id="fe22e-152">就 Linux 或 MacOS 而言，支援的 Azure 案例包括：</span><span class="sxs-lookup"><span data-stu-id="fe22e-152">For Linux or MacOS, main Azure scenarios that are supported:</span></span>

1. <span data-ttu-id="fe22e-153">使用 Azure 服務使用 Python hello 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="fe22e-153">Consuming Azure Services by using hello client libraries for Python</span></span>
2. <span data-ttu-id="fe22e-154">在 Linux VM 上執行應用程式</span><span class="sxs-lookup"><span data-stu-id="fe22e-154">Running your app in a Linux VM</span></span>
3. <span data-ttu-id="fe22e-155">開發和發佈 tooAzure 網站使用 Git</span><span class="sxs-lookup"><span data-stu-id="fe22e-155">Developing and publishing tooAzure Websites using Git</span></span>

<span data-ttu-id="fe22e-156">hello 第一個案例可讓您利用 hello Azure PaaS 功能例如 tooauthor 豐富的 web 應用程式[blob 儲存體](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，[佇列儲存體](storage/queues/storage-python-how-to-use-queue-storage.md)，[資料表儲存體](cosmos-db/table-storage-how-to-use-python.md)透過 hello Azure REST Api Pythonic 包裝函式等。</span><span class="sxs-lookup"><span data-stu-id="fe22e-156">hello first scenario enables you tooauthor rich web apps that take advantage of hello Azure PaaS capabilities such as [blob storage](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [queue storage](storage/queues/storage-python-how-to-use-queue-storage.md), [table storage](cosmos-db/table-storage-how-to-use-python.md) etc. via Pythonic wrappers for hello Azure REST APIs.</span></span> <span data-ttu-id="fe22e-157">這些 Web 應用程式在 Windows、Mac 和 Linux 上的運作方式相同。</span><span class="sxs-lookup"><span data-stu-id="fe22e-157">These work identically on Windows, Mac, and Linux.</span></span>  <span data-ttu-id="fe22e-158">您也可以從您的本機開發電腦或 Azure 上執行的 Linux VM，使用這些用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="fe22e-158">You can also use these client libraries from your local development machine or a Linux VM running on Azure.</span></span>

<span data-ttu-id="fe22e-159">Hello VM 案例中，您只要啟動您的選擇 （Ubuntu、 CentOS、 Suse） 的 Linux VM，並執行/管理您喜歡哪一點。</span><span class="sxs-lookup"><span data-stu-id="fe22e-159">For hello VM scenario, you simply start a Linux VM of your choice (Ubuntu, CentOS, Suse) and run/manage what you like.</span></span>  <span data-ttu-id="fe22e-160">例如，您可以執行[IPython] [ IPython] REPL/筆記本 Windows/Mac/Linux 電腦和您的瀏覽器 tooa Linux 或 Windows 多處理序執行中 VM hello IPython 引擎在 Azure 上的點上。</span><span class="sxs-lookup"><span data-stu-id="fe22e-160">As an example, you can run [IPython][IPython] REPL/notebook on your Windows/Mac/Linux machine and point your browser tooa Linux or Windows multi-proc VM running hello IPython Engine on Azure.</span></span>

<span data-ttu-id="fe22e-161">如需詳細資訊 tooset 設定 Linux VM，請參閱 hello[建立執行 Linux 之虛擬機器](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)教學課程。</span><span class="sxs-lookup"><span data-stu-id="fe22e-161">For information on how tooset up a Linux VM, see hello [Create a Virtual Machine Running Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tutorial.</span></span>

<span data-ttu-id="fe22e-162">使用 Git 部署，您可以開發 Python web 應用程式，並將它發行 tooan Azure 網站從任何作業系統。</span><span class="sxs-lookup"><span data-stu-id="fe22e-162">Using Git deployment, you can develop a Python web application and publish it tooan Azure Website from any operating system.</span></span>  <span data-ttu-id="fe22e-163">當您儲存機制 tooAzure，它會自動建立虛擬環境和 pip 安裝所需的封裝。</span><span class="sxs-lookup"><span data-stu-id="fe22e-163">When you push your repository tooAzure, it automatically creates a virtual environment and pip installs your required packages.</span></span>

<span data-ttu-id="fe22e-164">如需有關開發和發佈 Azure 網站的詳細資訊，請參閱 hello 的教學課程[建立網站 Django](app-service-web/web-sites-python-create-deploy-django-app.md)，[建立網站 Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md)，和[建立網站酒瓶](app-service-web/web-sites-python-create-deploy-flask-app.md)。</span><span class="sxs-lookup"><span data-stu-id="fe22e-164">For more information on developing and publishing Azure Websites, see hello tutorials for [Creating Websites with Django](app-service-web/web-sites-python-create-deploy-django-app.md), [Creating Websites with Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), and [Creating Websites with Flask](app-service-web/web-sites-python-create-deploy-flask-app.md).</span></span> <span data-ttu-id="fe22e-165">如需更多有關使用任何 WSGI 相容架構的一般資訊，請參閱[在 Azure 網站上設定 Python](app-service-web/web-sites-python-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="fe22e-165">For more general information on using any WSGI-compliant framework, see [Configuring Python with Azure Websites](app-service-web/web-sites-python-configure.md).</span></span>

## <a name="additional-software-and-resources"></a><span data-ttu-id="fe22e-166">其他軟體和資源：</span><span class="sxs-lookup"><span data-stu-id="fe22e-166">Additional Software and Resources:</span></span>
* [<span data-ttu-id="fe22e-167">Azure SDK for Python ReadTheDocs</span><span class="sxs-lookup"><span data-stu-id="fe22e-167">Azure SDK for Python ReadTheDocs</span></span>](http://azure-sdk-for-python.readthedocs.io/en/latest/)
* [<span data-ttu-id="fe22e-168">Azure SDK for Python GitHub</span><span class="sxs-lookup"><span data-stu-id="fe22e-168">Azure SDK for Python GitHub</span></span>](https://github.com/Azure/azure-sdk-for-python)
* [<span data-ttu-id="fe22e-169">適用於 Python 的官方 Azure 範例</span><span class="sxs-lookup"><span data-stu-id="fe22e-169">Official Azure samples for Python</span></span>](https://azure.microsoft.com/documentation/samples/?platform=python)
* <span data-ttu-id="fe22e-170">[Continuum Analytics Python 發佈][Continuum Analytics Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="fe22e-170">[Continuum Analytics Python Distribution][Continuum Analytics Python Distribution]</span></span>
* <span data-ttu-id="fe22e-171">[Enthought Python 發佈][Enthought Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="fe22e-171">[Enthought Python Distribution][Enthought Python Distribution]</span></span>
* <span data-ttu-id="fe22e-172">[ActiveState Python 發佈][ActiveState Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="fe22e-172">[ActiveState Python Distribution][ActiveState Python Distribution]</span></span>
* <span data-ttu-id="fe22e-173">[SciPy - Scientific Python 程式庫套件][SciPy - A suite of Scientific Python libraries]</span><span class="sxs-lookup"><span data-stu-id="fe22e-173">[SciPy - A suite of Scientific Python libraries][SciPy - A suite of Scientific Python libraries]</span></span>
* <span data-ttu-id="fe22e-174">[NumPy - Python 的數值程式庫][NumPy - A numerics library for Python]</span><span class="sxs-lookup"><span data-stu-id="fe22e-174">[NumPy - A numerics library for Python][NumPy - A numerics library for Python]</span></span>
* <span data-ttu-id="fe22e-175">[Django 專案 - 成熟的 Web 架構/CMS][Django Project - A mature web framework/CMS]</span><span class="sxs-lookup"><span data-stu-id="fe22e-175">[Django Project - A mature web framework/CMS][Django Project - A mature web framework/CMS]</span></span>
* <span data-ttu-id="fe22e-176">[IPython - 先進的 Python REPL/Notebook][IPython - an advanced REPL/Notebook for Python]</span><span class="sxs-lookup"><span data-stu-id="fe22e-176">[IPython - an advanced REPL/Notebook for Python][IPython - an advanced REPL/Notebook for Python]</span></span>
* <span data-ttu-id="fe22e-177">[GitHub 上適用於 Visual Studio 的 Python 工具][Python Tools for Visual Studio on GitHub]</span><span class="sxs-lookup"><span data-stu-id="fe22e-177">[Python Tools for Visual Studio on GitHub][Python Tools for Visual Studio on GitHub]</span></span>
* [<span data-ttu-id="fe22e-178">Python 開發人員中心</span><span class="sxs-lookup"><span data-stu-id="fe22e-178">Python Developer Center</span></span>](/develop/python/)

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
