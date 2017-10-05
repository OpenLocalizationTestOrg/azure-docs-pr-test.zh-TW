---
title: "安裝 Python 和 SDK - Azure"
description: "了解如何安裝 Python 和搭配 Azure 的 SDK。"
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
ms.openlocfilehash: c9df4e1f7677b2ed10684f6f3c981f2abf64f171
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="installing-python-and-the-sdk"></a><span data-ttu-id="1c031-103">安裝 Python 和 SDK</span><span class="sxs-lookup"><span data-stu-id="1c031-103">Installing Python and the SDK</span></span>
<span data-ttu-id="1c031-104">在 Windows 上設定 Python 相當簡單，而在 Mac、Linux 及[適用於 Windows 的 Bash](https://msdn.microsoft.com/commandline/wsl/about) 中則是已預先安裝 Python。</span><span class="sxs-lookup"><span data-stu-id="1c031-104">Python is easy to set up on Windows and comes pre-installed on Mac, Linux, and [Bash for Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span> <span data-ttu-id="1c031-105">本指南將逐步引導您完成安裝作業，並讓機器做好搭配 Azure 的準備。</span><span class="sxs-lookup"><span data-stu-id="1c031-105">This guide walks you through installation and getting your machine ready for use with Azure.</span></span>

## <a name="whats-in-the-python-azure-sdk"></a><span data-ttu-id="1c031-106">Python Azure SDK 含有哪些內容？</span><span class="sxs-lookup"><span data-stu-id="1c031-106">What's in the Python Azure SDK?</span></span>
<span data-ttu-id="1c031-107">Azure SDK for Python 內含的元件可讓您開發、部署及管理適用於 Azure 的 Python 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1c031-107">The Azure SDK for Python includes components that allow you to develop, deploy, and manage Python applications for Azure.</span></span> <span data-ttu-id="1c031-108">尤其是 Azure SDK for Python 包含下列各項：</span><span class="sxs-lookup"><span data-stu-id="1c031-108">Specifically, the Azure SDK for Python includes the following:</span></span>

* <span data-ttu-id="1c031-109">**管理程式庫**。</span><span class="sxs-lookup"><span data-stu-id="1c031-109">**Management libraries**.</span></span> <span data-ttu-id="1c031-110">這些類別庫提供一個可管理 Azure 資源 (例如儲存體帳戶、虛擬機器) 的介面。</span><span class="sxs-lookup"><span data-stu-id="1c031-110">These class libraries provide an interface managing Azure resources, such as storage accounts, virtual machines.</span></span>
* <span data-ttu-id="1c031-111">**執行階段程式庫**。</span><span class="sxs-lookup"><span data-stu-id="1c031-111">**Runtime libraries**.</span></span> <span data-ttu-id="1c031-112">這些類別庫提供一個可存取 Azure 功能 (例如儲存體和服務匯流排) 的介面。</span><span class="sxs-lookup"><span data-stu-id="1c031-112">These class libraries provide an interface for accessing Azure features, such as storage and service bus.</span></span>

## <a name="which-python-and-which-version-to-use"></a><span data-ttu-id="1c031-113">該使用哪個 Python 和哪個版本</span><span class="sxs-lookup"><span data-stu-id="1c031-113">Which Python and which version to use</span></span>
<span data-ttu-id="1c031-114">可用的 Python 解譯器有數種，範例包括：</span><span class="sxs-lookup"><span data-stu-id="1c031-114">There are several flavors of Python interpreters available - examples include:</span></span>

* <span data-ttu-id="1c031-115">CPython - 標準和最常見的 Python 解譯器</span><span class="sxs-lookup"><span data-stu-id="1c031-115">CPython - the standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="1c031-116">PyPy - CPython 的快速、相容替代實作</span><span class="sxs-lookup"><span data-stu-id="1c031-116">PyPy - fast, compliant alternative implementation to CPython</span></span>
* <span data-ttu-id="1c031-117">IronPython - 可在 .Net/CLR 上執行的 Python 解譯器</span><span class="sxs-lookup"><span data-stu-id="1c031-117">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="1c031-118">Jython - 可在「Java 虛擬機器」上執行的 Python 解譯器</span><span class="sxs-lookup"><span data-stu-id="1c031-118">Jython - Python interpreter that runs on the Java Virtual Machine</span></span>

<span data-ttu-id="1c031-119">**CPython** v2.7 或 v3.3+ 及 PyPy 5.4.0 已針對 Python Azure SDK 進行過測試並確定支援。</span><span class="sxs-lookup"><span data-stu-id="1c031-119">**CPython** v2.7 or v3.3+ and PyPy 5.4.0 are tested and supported for the Python Azure SDK.</span></span>

## <a name="where-to-get-python"></a><span data-ttu-id="1c031-120">可在哪裡取得 Python？</span><span class="sxs-lookup"><span data-stu-id="1c031-120">Where to get Python?</span></span>
<span data-ttu-id="1c031-121">取得 CPython 的方法有數種：</span><span class="sxs-lookup"><span data-stu-id="1c031-121">There are several ways to get CPython:</span></span>

* <span data-ttu-id="1c031-122">直接從 [www.python.org][www.python.org]</span><span class="sxs-lookup"><span data-stu-id="1c031-122">Directly from [www.python.org][www.python.org]</span></span>
* <span data-ttu-id="1c031-123">從聲譽良好的散發網站取得，如 [www.continuum.io][www.continuum.io]、[www.enthought.com][www.enthought.com] 或 [www.activestate.com][www.activestate.com]</span><span class="sxs-lookup"><span data-stu-id="1c031-123">From a reputable distro such as [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] or [www.activestate.com][www.activestate.com]</span></span>
* <span data-ttu-id="1c031-124">從原始碼組建！</span><span class="sxs-lookup"><span data-stu-id="1c031-124">Build from source!</span></span>

<span data-ttu-id="1c031-125">除非您有特定的需求，否則我們建議您採用前兩個選項。</span><span class="sxs-lookup"><span data-stu-id="1c031-125">Unless you have a specific need, we recommend the first two options.</span></span>

## <a name="sdk-installation-on-windows-linux-and-macos-client-libraries-only"></a><span data-ttu-id="1c031-126">Windows、Linux 及 MacOS 上的 SDK 安裝 (僅限用戶端程式庫)</span><span class="sxs-lookup"><span data-stu-id="1c031-126">SDK Installation on Windows, Linux, and MacOS (client libraries only)</span></span>
<span data-ttu-id="1c031-127">如果您已經安裝 Python，您可以使用 PIP 在現有的 Python 2.7 或 Python 3.3+ 環境中，安裝所有用戶端程式的組合。</span><span class="sxs-lookup"><span data-stu-id="1c031-127">If you already have Python installed, you can use pip to install a bundle of all the client libraries in your existing Python 2.7 or Python 3.3+ environment.</span></span> <span data-ttu-id="1c031-128">此作業會從 [Python 套件索引][Python Package Index] (PyPI) 下載套件。</span><span class="sxs-lookup"><span data-stu-id="1c031-128">This downloads the packages from the [Python Package Index][Python Package Index] (PyPI).</span></span>

<span data-ttu-id="1c031-129">您可能需要系統管理員權限：</span><span class="sxs-lookup"><span data-stu-id="1c031-129">You may need administrator rights:</span></span>

* <span data-ttu-id="1c031-130">Linux 和 MacOS：使用 `sudo` 命令︰`sudo pip install azure-mgmt-compute`。</span><span class="sxs-lookup"><span data-stu-id="1c031-130">Linux and MacOS, use the `sudo` command: `sudo pip install azure-mgmt-compute`.</span></span>
* <span data-ttu-id="1c031-131">Windows：以系統管理員身分開啟 PowerShell/命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="1c031-131">Windows: open your PowerShell/Command prompt as an administrator</span></span>

<span data-ttu-id="1c031-132">您可以為每個 Azure 服務個別安裝程式庫：</span><span class="sxs-lookup"><span data-stu-id="1c031-132">You can install individually each library for each Azure service:</span></span>

```console
   $ pip install azure-batch          # Install the latest Batch runtime library
   $ pip install azure-mgmt-scheduler # Install the latest Storage management library
```

<span data-ttu-id="1c031-133">可以使用 `--pre` 旗標來安裝預覽版套件︰</span><span class="sxs-lookup"><span data-stu-id="1c031-133">Preview packages can be installed using the `--pre` flag:</span></span>

```console
   $ pip install --pre azure-mgmt-compute # installs only the latest Compute Management library
```

<span data-ttu-id="1c031-134">您也可以在單行中使用 `azure` 中繼套件來安裝一組 Azure 程式庫。</span><span class="sxs-lookup"><span data-stu-id="1c031-134">You can also install a set of Azure libraries in a single line using the `azure` meta-package.</span></span> <span data-ttu-id="1c031-135">由於此中繼套件中並非所有套件都已發佈為穩定版，因此 `azure` 中繼套件仍處於預覽版狀態。</span><span class="sxs-lookup"><span data-stu-id="1c031-135">Since not all packages in this meta-package are published as stable yet, the `azure` meta-package is still in preview.</span></span>
<span data-ttu-id="1c031-136">不過，從程式碼品質/完整性的觀點來看，目前可以將核心套件視為「穩定版」。</span><span class="sxs-lookup"><span data-stu-id="1c031-136">However, the core packages, from code quality/completeness perspectives can be considered "stable" at this time</span></span>

* <span data-ttu-id="1c031-137">我們會儘快將它正式標示為穩定版以與其他語言一致。</span><span class="sxs-lookup"><span data-stu-id="1c031-137">it is officially labeled as such in sync with other languages as soon as possible.</span></span>
  <span data-ttu-id="1c031-138">在那之前，我們不打算進行任何進一步的重大變更。</span><span class="sxs-lookup"><span data-stu-id="1c031-138">We are not planning on any further major changes until then.</span></span>

<span data-ttu-id="1c031-139">由於它是預覽版，因此您必須使用 `--pre` 旗標︰</span><span class="sxs-lookup"><span data-stu-id="1c031-139">Since it's a preview release, you need to use the `--pre` flag:</span></span>

```console
   $ pip install --pre azure
```

<span data-ttu-id="1c031-140">或直接使用</span><span class="sxs-lookup"><span data-stu-id="1c031-140">or directly</span></span>

```console
   $ pip install azure==2.0.0rc6
```

## <a name="getting-more-packages"></a><span data-ttu-id="1c031-141">取得更多封裝</span><span class="sxs-lookup"><span data-stu-id="1c031-141">Getting More Packages</span></span>
<span data-ttu-id="1c031-142">[Python 封裝索引][Python Package Index] (PyPI) 具有選擇性豐富的 Python 程式庫。</span><span class="sxs-lookup"><span data-stu-id="1c031-142">The [Python Package Index][Python Package Index] (PyPI) has a rich selection of Python libraries.</span></span>  <span data-ttu-id="1c031-143">如果您選擇了安裝散發版本，則您將已擁有從 Web 開發到「工程運算」的各種案例中大多數令人關注的部分。</span><span class="sxs-lookup"><span data-stu-id="1c031-143">If you chose to install a Distro, you'll already have most of the interesting bits for various scenarios from web development to Technical Computing.</span></span>

## <a name="python-tools-for-visual-studio"></a><span data-ttu-id="1c031-144">Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1c031-144">Python Tools for Visual Studio</span></span>
<span data-ttu-id="1c031-145">[適用於 Visual Studio 的 Python 工具][適用於 Visual Studio 的 Python 工具] (PTVS) 是 Microsoft 提供的免費/OSS 外掛程式，它能將 VS 轉變為成熟的 Python IDE：</span><span class="sxs-lookup"><span data-stu-id="1c031-145">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) is a free/OSS plugin from Microsoft, which turns VS into a full-fledged Python IDE:</span></span>

![how-to-install-python-ptvs](./media/python-how-to-install/how-to-install-python-ptvs.png)

<span data-ttu-id="1c031-147">您可以選擇是否要使用 PTVS，不過我們建議您使用，因為它能提供 Python 和 Web 專案/方案支援、偵錯、分析、互動式視窗、範本編輯和 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="1c031-147">Using PTVS is optional, but is recommended as it gives you Python and Web Project/Solution support, debugging, profiling, interactive window, Template editing, and Intellisense.</span></span>

<span data-ttu-id="1c031-148">PTVS 也能讓您使用部署至[雲端服務](cloud-services/cloud-services-python-ptvs.md)和[網站](app-service-web/web-sites-python-ptvs-django-mysql.md)的支援，輕鬆部署至 Microsoft Azure。</span><span class="sxs-lookup"><span data-stu-id="1c031-148">PTVS also makes it easy to deploy to Microsoft Azure, with support for deployment to [Cloud Services](cloud-services/cloud-services-python-ptvs.md) and [Websites](app-service-web/web-sites-python-ptvs-django-mysql.md).</span></span>

<span data-ttu-id="1c031-149">PTVS 可以和您現有的 Visual Studio 2013、2015 或 2017 安裝一同運作。</span><span class="sxs-lookup"><span data-stu-id="1c031-149">PTVS works with your existing Visual Studio 2013, 2015, or 2017 installation.</span></span>  <span data-ttu-id="1c031-150">如需文件、下載項目和相關討論，請參閱[適用於 Visual Studio 的 Python 工具]。</span><span class="sxs-lookup"><span data-stu-id="1c031-150">For documentation, downloads and discussions, see [Python Tools for Visual Studio].</span></span>  

## <a name="python-azure-scenarios-for-linux-and-macos"></a><span data-ttu-id="1c031-151">適用於 Linux 和 MacOS 的 Python Azure 案例</span><span class="sxs-lookup"><span data-stu-id="1c031-151">Python Azure Scenarios for Linux and MacOS</span></span>
<span data-ttu-id="1c031-152">就 Linux 或 MacOS 而言，支援的 Azure 案例包括：</span><span class="sxs-lookup"><span data-stu-id="1c031-152">For Linux or MacOS, main Azure scenarios that are supported:</span></span>

1. <span data-ttu-id="1c031-153">使用 Python 的用戶端程式庫取用 Azure 服務</span><span class="sxs-lookup"><span data-stu-id="1c031-153">Consuming Azure Services by using the client libraries for Python</span></span>
2. <span data-ttu-id="1c031-154">在 Linux VM 上執行應用程式</span><span class="sxs-lookup"><span data-stu-id="1c031-154">Running your app in a Linux VM</span></span>
3. <span data-ttu-id="1c031-155">使用 Git 開發和發佈至 Azure 網站</span><span class="sxs-lookup"><span data-stu-id="1c031-155">Developing and publishing to Azure Websites using Git</span></span>

<span data-ttu-id="1c031-156">第一個案例可讓您撰寫能透過 Azure REST API 的 Python 風格包裝函式利用 Azure PaaS 功能 (例如 [Blob 儲存體](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)、[佇列儲存體](storage/queues/storage-python-how-to-use-queue-storage.md)、[資料表儲存體](cosmos-db/table-storage-how-to-use-python.md)等) 的豐富 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1c031-156">The first scenario enables you to author rich web apps that take advantage of the Azure PaaS capabilities such as [blob storage](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [queue storage](storage/queues/storage-python-how-to-use-queue-storage.md), [table storage](cosmos-db/table-storage-how-to-use-python.md) etc. via Pythonic wrappers for the Azure REST APIs.</span></span> <span data-ttu-id="1c031-157">這些 Web 應用程式在 Windows、Mac 和 Linux 上的運作方式相同。</span><span class="sxs-lookup"><span data-stu-id="1c031-157">These work identically on Windows, Mac, and Linux.</span></span>  <span data-ttu-id="1c031-158">您也可以從您的本機開發電腦或 Azure 上執行的 Linux VM，使用這些用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="1c031-158">You can also use these client libraries from your local development machine or a Linux VM running on Azure.</span></span>

<span data-ttu-id="1c031-159">對於 VM 案例，您只需要啟動選擇的 Linux VM (Ubuntu、CentOS、Suse)，便能執行/管理所需的項目。</span><span class="sxs-lookup"><span data-stu-id="1c031-159">For the VM scenario, you simply start a Linux VM of your choice (Ubuntu, CentOS, Suse) and run/manage what you like.</span></span>  <span data-ttu-id="1c031-160">例如，您可以在 Windows/Mac/Linux 機器上執行 [IPython][IPython] REPL/notebook，然後將瀏覽器指向在 Azure 上執行 IPython Engine 的 Linux 或 Windows 多重處理器 VM。</span><span class="sxs-lookup"><span data-stu-id="1c031-160">As an example, you can run [IPython][IPython] REPL/notebook on your Windows/Mac/Linux machine and point your browser to a Linux or Windows multi-proc VM running the IPython Engine on Azure.</span></span>

<span data-ttu-id="1c031-161">如需如何設定 Linux VM 的資訊，請參閱[建立執行 Linux 的虛擬機器](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)教學課程。</span><span class="sxs-lookup"><span data-stu-id="1c031-161">For information on how to set up a Linux VM, see the [Create a Virtual Machine Running Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tutorial.</span></span>

<span data-ttu-id="1c031-162">您可以使用 Git 部署開發 Python Ｗeb 應用程式，並從任何作業系統將其發佈至 Azure 網站中。</span><span class="sxs-lookup"><span data-stu-id="1c031-162">Using Git deployment, you can develop a Python web application and publish it to an Azure Website from any operating system.</span></span>  <span data-ttu-id="1c031-163">當您將您的存放庫推送至 Azure 時，就會自動建立虛擬環境和 pip 安裝所需的套件。</span><span class="sxs-lookup"><span data-stu-id="1c031-163">When you push your repository to Azure, it automatically creates a virtual environment and pip installs your required packages.</span></span>

<span data-ttu-id="1c031-164">如需有關開發和發佈「Azure 網站」的詳細資訊，請參閱[使用 Django 建立網站](app-service-web/web-sites-python-create-deploy-django-app.md)、[使用 Bottle 建立網站](app-service-web/web-sites-python-create-deploy-bottle-app.md)及[使用 Flask 建立網站](app-service-web/web-sites-python-create-deploy-flask-app.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="1c031-164">For more information on developing and publishing Azure Websites, see the tutorials for [Creating Websites with Django](app-service-web/web-sites-python-create-deploy-django-app.md), [Creating Websites with Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), and [Creating Websites with Flask](app-service-web/web-sites-python-create-deploy-flask-app.md).</span></span> <span data-ttu-id="1c031-165">如需更多有關使用任何 WSGI 相容架構的一般資訊，請參閱[在 Azure 網站上設定 Python](app-service-web/web-sites-python-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="1c031-165">For more general information on using any WSGI-compliant framework, see [Configuring Python with Azure Websites](app-service-web/web-sites-python-configure.md).</span></span>

## <a name="additional-software-and-resources"></a><span data-ttu-id="1c031-166">其他軟體和資源：</span><span class="sxs-lookup"><span data-stu-id="1c031-166">Additional Software and Resources:</span></span>
* [<span data-ttu-id="1c031-167">Azure SDK for Python ReadTheDocs</span><span class="sxs-lookup"><span data-stu-id="1c031-167">Azure SDK for Python ReadTheDocs</span></span>](http://azure-sdk-for-python.readthedocs.io/en/latest/)
* [<span data-ttu-id="1c031-168">Azure SDK for Python GitHub</span><span class="sxs-lookup"><span data-stu-id="1c031-168">Azure SDK for Python GitHub</span></span>](https://github.com/Azure/azure-sdk-for-python)
* [<span data-ttu-id="1c031-169">適用於 Python 的官方 Azure 範例</span><span class="sxs-lookup"><span data-stu-id="1c031-169">Official Azure samples for Python</span></span>](https://azure.microsoft.com/documentation/samples/?platform=python)
* <span data-ttu-id="1c031-170">[Continuum Analytics Python 發佈][Continuum Analytics Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="1c031-170">[Continuum Analytics Python Distribution][Continuum Analytics Python Distribution]</span></span>
* <span data-ttu-id="1c031-171">[Enthought Python 發佈][Enthought Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="1c031-171">[Enthought Python Distribution][Enthought Python Distribution]</span></span>
* <span data-ttu-id="1c031-172">[ActiveState Python 發佈][ActiveState Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="1c031-172">[ActiveState Python Distribution][ActiveState Python Distribution]</span></span>
* <span data-ttu-id="1c031-173">[SciPy - Scientific Python 程式庫套件][SciPy - A suite of Scientific Python libraries]</span><span class="sxs-lookup"><span data-stu-id="1c031-173">[SciPy - A suite of Scientific Python libraries][SciPy - A suite of Scientific Python libraries]</span></span>
* <span data-ttu-id="1c031-174">[NumPy - Python 的數值程式庫][NumPy - A numerics library for Python]</span><span class="sxs-lookup"><span data-stu-id="1c031-174">[NumPy - A numerics library for Python][NumPy - A numerics library for Python]</span></span>
* <span data-ttu-id="1c031-175">[Django 專案 - 成熟的 Web 架構/CMS][Django Project - A mature web framework/CMS]</span><span class="sxs-lookup"><span data-stu-id="1c031-175">[Django Project - A mature web framework/CMS][Django Project - A mature web framework/CMS]</span></span>
* <span data-ttu-id="1c031-176">[IPython - 先進的 Python REPL/Notebook][IPython - an advanced REPL/Notebook for Python]</span><span class="sxs-lookup"><span data-stu-id="1c031-176">[IPython - an advanced REPL/Notebook for Python][IPython - an advanced REPL/Notebook for Python]</span></span>
* <span data-ttu-id="1c031-177">[GitHub 上適用於 Visual Studio 的 Python 工具][Python Tools for Visual Studio on GitHub]</span><span class="sxs-lookup"><span data-stu-id="1c031-177">[Python Tools for Visual Studio on GitHub][Python Tools for Visual Studio on GitHub]</span></span>
* [<span data-ttu-id="1c031-178">Python 開發人員中心</span><span class="sxs-lookup"><span data-stu-id="1c031-178">Python Developer Center</span></span>](/develop/python/)

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
[Setting up a Linux VM via the Azure portal]: create-and-configure-opensuse-vm-in-portal.md
[How to use the Azure Command-Line Interface]: crossplat-cmd-tools.md
[Create a Virtual Machine Running Linux]: virtual-machines-linux-quick-create-cli.md
[Creating Websites with Django]: web-sites-python-create-deploy-django-app.md
[Creating Websites with Bottle]: web-sites-python-create-deploy-bottle-app.md
[Creating Websites with Flask]: web-sites-python-create-deploy-flask-app.md
[Configuring Python with Azure Websites]: web-sites-python-configure.md
[table storage]: storage-python-how-to-use-table-storage.md
[queue storage]: storage-python-how-to-use-queue-storage.md
[blob storage]:storage/blobs/storage-python-how-to-use-blob-storage.md
