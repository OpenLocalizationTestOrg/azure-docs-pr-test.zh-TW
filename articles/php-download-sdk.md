---
title: aaaDownload hello Azure SDK for PHP
description: "了解如何 toodownload 並安裝 hello Azure SDK for PHP。"
documentationcenter: php
services: app-service\web
author: allclark
manager: douge
editor: 
ms.assetid: bac355ac-4c25-42f4-8273-c5112eafa8d4
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 06/01/2016
ms.author: allclark;yaqiyang
ms.openlocfilehash: 94f56fc4f91bb175c08b9f7a43cb221c827694a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-azure-sdk-for-php"></a><span data-ttu-id="bc362-103">下載 hello Azure SDK for PHP</span><span class="sxs-lookup"><span data-stu-id="bc362-103">Download hello Azure SDK for PHP</span></span>
## <a name="overview"></a><span data-ttu-id="bc362-104">概觀</span><span class="sxs-lookup"><span data-stu-id="bc362-104">Overview</span></span>
<span data-ttu-id="bc362-105">hello Azure SDK for PHP 包含 toodevelop 可讓您的元件、 部署和管理 Azure 的 PHP 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bc362-105">hello Azure SDK for PHP includes components that allow you toodevelop, deploy, and manage PHP applications for Azure.</span></span> <span data-ttu-id="bc362-106">具體來說，hello Azure SDK for PHP 包含 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="bc362-106">Specifically, hello Azure SDK for PHP includes hello following:</span></span>

* <span data-ttu-id="bc362-107">**Azure 的 hello PHP 用戶端程式庫**。</span><span class="sxs-lookup"><span data-stu-id="bc362-107">**hello PHP client libraries for Azure**.</span></span> <span data-ttu-id="bc362-108">這些類別庫所提供的介面可供存取 Azure 功能，例如資料管理服務和雲端服務。</span><span class="sxs-lookup"><span data-stu-id="bc362-108">These class libraries provide an interface for accessing Azure features, such as data management services and cloud services.</span></span>  
* <span data-ttu-id="bc362-109">**hello Mac、 Linux 及 Windows (Azure CLI) 的 Azure 命令列介面**。</span><span class="sxs-lookup"><span data-stu-id="bc362-109">**hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)**.</span></span> <span data-ttu-id="bc362-110">這是一組命令，可用於部署和管理 Azure 服務，例如 Azure 網站和 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bc362-110">This is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="bc362-111">hello Azure CLI 任何平台，包括 Mac、 Linux 及 Windows 上的工作。</span><span class="sxs-lookup"><span data-stu-id="bc362-111">hello Azure CLI work on any platform, including Mac, Linux, and Windows.</span></span>
* <span data-ttu-id="bc362-112">**Azure PowerShell (僅限 Windows)**。</span><span class="sxs-lookup"><span data-stu-id="bc362-112">**Azure PowerShell (Windows Only)**.</span></span> <span data-ttu-id="bc362-113">這是一組 PowerShell Cmdlet，可用於部署和管理 Azure 服務，例如雲端服務和虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bc362-113">This is a set of PowerShell cmdlets for deploying and managing Azure Services, such as Cloud Services and Virtual Machines.</span></span>
* <span data-ttu-id="bc362-114">**hello （僅限 Windows） Azure 模擬器**。</span><span class="sxs-lookup"><span data-stu-id="bc362-114">**hello Azure Emulators (Windows Only)**.</span></span> <span data-ttu-id="bc362-115">hello 計算和儲存體模擬器是雲端服務和資料管理服務可讓您 tootest 本機應用程式的本機模擬器。</span><span class="sxs-lookup"><span data-stu-id="bc362-115">hello compute and storage emulators are local emulators of cloud services and data management services that allow you tootest an application locally.</span></span> <span data-ttu-id="bc362-116">hello Azure 模擬器上執行 Windows 只。</span><span class="sxs-lookup"><span data-stu-id="bc362-116">hello Azure Emulators run on Windows only.</span></span>

<span data-ttu-id="bc362-117">hello 下列各節說明 toodownload 並安裝 hello 上面所述的元件。</span><span class="sxs-lookup"><span data-stu-id="bc362-117">hello sections below describe how toodownload and install hello components described above.</span></span>

<span data-ttu-id="bc362-118">hello 本主題中的指示假設您有[PHP] [ install-php]安裝。</span><span class="sxs-lookup"><span data-stu-id="bc362-118">hello instructions in this topic assume that you have [PHP][install-php] installed.</span></span>

> [!NOTE]
> <span data-ttu-id="bc362-119">適用於 Azure，您必須擁有 PHP 5.5 或更新版本 toouse hello PHP 用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="bc362-119">You must have PHP 5.5 or higher toouse hello PHP client libraries for Azure.</span></span>
> 
> 

## <a name="php-client-libraries-for-azure"></a><span data-ttu-id="bc362-120">適用於 Azure 的 PHP 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="bc362-120">PHP client libraries for Azure</span></span>
<span data-ttu-id="bc362-121">Azure 的 hello PHP 用戶端程式庫提供介面來存取 Azure 的功能，例如資料管理服務和雲端服務，從任何作業系統。</span><span class="sxs-lookup"><span data-stu-id="bc362-121">hello PHP Client Libraries for Azure provide an interface for accessing Azure features, such as data management services and cloud services, from any operating system.</span></span> <span data-ttu-id="bc362-122">可以透過 hello 編輯器安裝這些程式庫。</span><span class="sxs-lookup"><span data-stu-id="bc362-122">These libraries can be installed via hello Composer.</span></span>

<span data-ttu-id="bc362-123">如需如何 toouse hello azure 的 PHP 用戶端程式庫的資訊，請參閱[tooUse hello Blob 服務的方式][blob-service]， [tooUse hello 表格服務的方式][ table-service]和[tooUse hello 佇列服務的方式][queue-service]。</span><span class="sxs-lookup"><span data-stu-id="bc362-123">For information about how toouse hello PHP Client Libraries for Azure, see [How tooUse hello Blob Service][blob-service], [How tooUse hello Table Service][table-service] and [How tooUse hello Queue Service][queue-service].</span></span>

### <a name="install-via-composer"></a><span data-ttu-id="bc362-124">透過編輯器安裝</span><span class="sxs-lookup"><span data-stu-id="bc362-124">Install via Composer</span></span>
1. <span data-ttu-id="bc362-125">[安裝 Git][install-git]。</span><span class="sxs-lookup"><span data-stu-id="bc362-125">[Install Git][install-git].</span></span>

    > [AZURE.NOTE] <span data-ttu-id="bc362-126">在 Windows 中，您也需要 tooadd hello Git 可執行檔 tooyour PATH 環境變數。</span><span class="sxs-lookup"><span data-stu-id="bc362-126">On Windows, you will also need tooadd hello Git executable tooyour PATH environment variable.</span></span>

1. <span data-ttu-id="bc362-127">建立名為**composer.json**在 hello 您專案的根目錄，並加入下列程式碼 tooit hello:</span><span class="sxs-lookup"><span data-stu-id="bc362-127">Create a file named **composer.json** in hello root of your project and add hello following code tooit:</span></span>
   
        {
            "require": {
                "microsoft/windowsazure": "^0.4"
            }
        }
2. <span data-ttu-id="bc362-128">將 **[composer.phar][composer-phar]** 下載到專案根目錄中。</span><span class="sxs-lookup"><span data-stu-id="bc362-128">Download **[composer.phar][composer-phar]** in your project root.</span></span>
3. <span data-ttu-id="bc362-129">開啟命令提示字元，在專案根目錄中執行此命令</span><span class="sxs-lookup"><span data-stu-id="bc362-129">Open a command prompt and execute this in your project root</span></span>
   
        php composer.phar install

## <a name="azure-powershell-and-azure-emulators"></a><span data-ttu-id="bc362-130">Azure PowerShell 和 Azure 模擬器</span><span class="sxs-lookup"><span data-stu-id="bc362-130">Azure PowerShell and Azure Emulators</span></span>
<span data-ttu-id="bc362-131">Azure PowerShell 是一組 PowerShell Cmdlet，可用於部署和管理 Azure 服務 (例如雲端服務和虛擬機器)。</span><span class="sxs-lookup"><span data-stu-id="bc362-131">Azure PowerShell is a set of PowerShell cmdlets for deploying and managing Azure Services (such as Cloud Services and Virtual Machines).</span></span> <span data-ttu-id="bc362-132">hello Azure 模擬器是雲端服務和資料管理服務可讓您 tootest 本機應用程式的模擬器。</span><span class="sxs-lookup"><span data-stu-id="bc362-132">hello Azure Emulators are emulators of cloud services and data management services that allow you tootest an application locally.</span></span> <span data-ttu-id="bc362-133">只有 Windows 支援這些元件。</span><span class="sxs-lookup"><span data-stu-id="bc362-133">These components are supported Windows only.</span></span>

<span data-ttu-id="bc362-134">hello 建議 tooinstall Azure PowerShell 和 hello Azure 模擬器為 toouse hello [Microsoft Web Platform Installer][download-wpi]。</span><span class="sxs-lookup"><span data-stu-id="bc362-134">hello recommended way tooinstall Azure PowerShell and hello Azure Emulators is toouse hello [Microsoft Web Platform Installer][download-wpi].</span></span> <span data-ttu-id="bc362-135">請注意，您也可以選擇 tooinstall 其他開發元件，例如 PHP、 SQL Server、 hello Microsoft Drivers for PHP 和 WebMatrix 的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="bc362-135">Note that you can also choose tooinstall other development components, such as PHP, SQL Server, hello Microsoft Drivers for SQL Server for PHP, and WebMatrix.</span></span>

<span data-ttu-id="bc362-136">如需有關資訊 toouse Azure PowerShell，請參閱[如何 tooUse Azure PowerShell][powershell-tools]。</span><span class="sxs-lookup"><span data-stu-id="bc362-136">For information about how toouse Azure PowerShell, see [How tooUse Azure PowerShell][powershell-tools].</span></span>

## <a name="azure-cli"></a><span data-ttu-id="bc362-137">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bc362-137">Azure CLI</span></span>
<span data-ttu-id="bc362-138">hello Azure CLI 是一組命令用來部署和管理 Azure 服務，例如 Azure 網站和 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bc362-138">hello Azure CLI is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="bc362-139">如需安裝 Azure CLI 資訊，請參閱[安裝 hello Azure CLI](cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="bc362-139">For information about installing Azure CLI, see [Install hello Azure CLI](cli-install-nodejs.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc362-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bc362-140">Next steps</span></span>
<span data-ttu-id="bc362-141">如需詳細資訊，請參閱 hello [PHP 開發人員中心](/develop/php/)。</span><span class="sxs-lookup"><span data-stu-id="bc362-141">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[composer-github]: https://github.com/composer/composer
[composer-phar]: http://getcomposer.org/composer.phar
[nodejs-org]: http://nodejs.org/
[install-node-linux]: https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager
[download-wpi]: http://go.microsoft.com/fwlink/?LinkId=253447
[mac-installer]: http://go.microsoft.com/fwlink/?LinkId=252249
[blob-service]: http://go.microsoft.com/fwlink/?LinkId=252714
[table-service]: http://go.microsoft.com/fwlink/?LinkId=252715
[queue-service]: http://go.microsoft.com/fwlink/?LinkId=252716
[azure cli]: http://go.microsoft.com/fwlink/?LinkId=252717
[powershell-tools]: http://go.microsoft.com/fwlink/?LinkId=252718
[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
