---
title: "建立虛擬機器映像的 hello Azure Marketplace aaaTechnical 必要條件 |Microsoft 文件"
description: "了解建立及部署虛擬機器映像 toohello Azure Marketplace 供其他人的 hello 需求 toopurchase。"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 63c16966-0304-4b17-a715-368a0a5ccb2c
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: fcae4d9e052581e3c1dfe7962e6d50ec31040419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="technical-prerequisites-for-creating-a-virtual-machine-image-for-hello-azure-marketplace"></a><span data-ttu-id="8e7e4-103">技術建立虛擬機器映像的 hello Azure Marketplace 的必要條件</span><span class="sxs-lookup"><span data-stu-id="8e7e4-103">Technical prerequisites for creating a virtual machine image for hello Azure Marketplace</span></span>
<span data-ttu-id="8e7e4-104">閱讀 hello 程序開始前，徹底，並了解為何，會執行每個步驟。</span><span class="sxs-lookup"><span data-stu-id="8e7e4-104">Read hello process thoroughly before beginning and understand where and why each step is performed.</span></span> <span data-ttu-id="8e7e4-105">盡量，您應該準備您的公司資訊和其他資料，下載必要的工具和/或建立技術元件開始 hello 供應項目建立處理程序之前。</span><span class="sxs-lookup"><span data-stu-id="8e7e4-105">As much as possible, you should prepare your company information and other data, download necessary tools, and/or create technical components before beginning hello offer creation process.</span></span> <span data-ttu-id="8e7e4-106">檢閱本文之後，您會更清楚這些項目。</span><span class="sxs-lookup"><span data-stu-id="8e7e4-106">These items should be clear from reviewing this article.</span></span>  

## <a name="download-needed-tools--applications"></a><span data-ttu-id="8e7e4-107">下載需要的工具和應用程式</span><span class="sxs-lookup"><span data-stu-id="8e7e4-107">Download needed tools & applications</span></span>
<span data-ttu-id="8e7e4-108">您應該有下列項目之後，再開始 hello 程序的 hello:</span><span class="sxs-lookup"><span data-stu-id="8e7e4-108">You should have hello following items ready before beginning hello process:</span></span>

* <span data-ttu-id="8e7e4-109">根據您的目標、 安裝 hello [Azure PowerShell cmdlet](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids)或[Linux 命令列介面工具](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409)從 hello [Azure 下載](https://azure.microsoft.com/downloads/)頁面。</span><span class="sxs-lookup"><span data-stu-id="8e7e4-109">Depending on which operating system you are targeting, install hello [Azure PowerShell cmdlets](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) or [Linux command-line interface tool](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) from hello [Azure Downloads](https://azure.microsoft.com/downloads/) page.</span></span>
* <span data-ttu-id="8e7e4-110">從 CodePlex 安裝 Azure 儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="8e7e4-110">Install Azure Storage Explorer from CodePlex.</span></span>
* <span data-ttu-id="8e7e4-111">下載並安裝適用於 Azure 認證 hello 憑證測試工具：</span><span class="sxs-lookup"><span data-stu-id="8e7e4-111">Download and install hello Certification Test Tool for Azure Certified:</span></span>
  * <span data-ttu-id="8e7e4-112">[http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913)。</span><span class="sxs-lookup"><span data-stu-id="8e7e4-112">[http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913).</span></span> <span data-ttu-id="8e7e4-113">您需要 Windows 型電腦 toorun hello 憑證 」 工具。</span><span class="sxs-lookup"><span data-stu-id="8e7e4-113">You need a Windows-based computer toorun hello certification tool.</span></span> <span data-ttu-id="8e7e4-114">如果您沒有可用的 Windows 電腦，您可以執行使用 Windows 架構的 VM 在 Azure 中的 hello 工具。</span><span class="sxs-lookup"><span data-stu-id="8e7e4-114">If you do not have a Windows-based computer available, you can run hello tool using a Windows-based VM in Azure.</span></span>

## <a name="platforms-supported"></a><span data-ttu-id="8e7e4-115">支援的平台</span><span class="sxs-lookup"><span data-stu-id="8e7e4-115">Platforms supported</span></span>
<span data-ttu-id="8e7e4-116">您可以在 Windows 或 Linux 上開發 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="8e7e4-116">You can develop Azure-based VMs on Windows or Linux.</span></span> <span data-ttu-id="8e7e4-117">Hello 發行程序-例如建立 Azure 相容的虛擬硬碟 (VHD)-使用不同的工具和步驟的作業系統根據您使用的某些項目：</span><span class="sxs-lookup"><span data-stu-id="8e7e4-117">Some elements of hello publishing process--such as creating an Azure-compatible virtual hard disk (VHD)--use different tools and steps depending on which operating system you are using:</span></span>  

* <span data-ttu-id="8e7e4-118">如果您使用 Linux，請參閱"toohello 建立相容的 Azure VHD （以 Linux 為基礎） > 一節的 hello[虛擬機器映像發佈指南](marketplace-publishing-vm-image-creation.md)。</span><span class="sxs-lookup"><span data-stu-id="8e7e4-118">If you are using Linux, refer toohello “Create an Azure-compatible VHD (Linux-based)” section of hello [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md).</span></span>
* <span data-ttu-id="8e7e4-119">如果您使用 Windows 時，請參閱"toohello 建立相容的 Azure VHD （以 Windows 為基礎） > 一節的 hello[虛擬機器映像發佈指南](marketplace-publishing-vm-image-creation.md)。</span><span class="sxs-lookup"><span data-stu-id="8e7e4-119">If you are using Windows, refer toohello “Create an Azure-compatible VHD (Windows-based)” section of hello [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md).</span></span>

> [!NOTE]
> <span data-ttu-id="8e7e4-120">您需要存取 tooa Windows 為基礎的電腦：</span><span class="sxs-lookup"><span data-stu-id="8e7e4-120">You need access tooa Windows-based machine to:</span></span>
> 
> * <span data-ttu-id="8e7e4-121">執行 hello 憑證驗證工具。</span><span class="sxs-lookup"><span data-stu-id="8e7e4-121">Run hello certification validation tool.</span></span>
> * <span data-ttu-id="8e7e4-122">建立 hello VHD 憑證送出 hello VHD 共用存取簽章 URL。</span><span class="sxs-lookup"><span data-stu-id="8e7e4-122">Create hello VHD shared access signature URL for hello VHD certification submission.</span></span>
> 
> 

## <a name="develop-your-vhd"></a><span data-ttu-id="8e7e4-123">開發您的 VHD</span><span class="sxs-lookup"><span data-stu-id="8e7e4-123">Develop your VHD</span></span>
<span data-ttu-id="8e7e4-124">您可以開發 Azure Vhd hello 雲端或內部部署中：</span><span class="sxs-lookup"><span data-stu-id="8e7e4-124">You can develop Azure VHDs in hello cloud or on-premises:</span></span>

* <span data-ttu-id="8e7e4-125">雲端開發表示所有開發步驟都會在 Azure 的 VHD 上遠端執行。</span><span class="sxs-lookup"><span data-stu-id="8e7e4-125">Cloud-based development means all development steps are performed remotely on a VHD resident on Azure.</span></span>
* <span data-ttu-id="8e7e4-126">內部部署開發則需要使用內部部署基礎結構下載 VHD 和開發。</span><span class="sxs-lookup"><span data-stu-id="8e7e4-126">On-premises development requires downloading a VHD and developing it using on-premises infrastructure.</span></span> <span data-ttu-id="8e7e4-127">雖然可行，但我們不建議您這麼做。</span><span class="sxs-lookup"><span data-stu-id="8e7e4-127">Although this is possible, we do not recommend it.</span></span> <span data-ttu-id="8e7e4-128">請注意，開發 Windows 或 SQL 的內部部署需要您 toohave hello 相關的內部部署授權金鑰。</span><span class="sxs-lookup"><span data-stu-id="8e7e4-128">Note that developing for Windows or SQL on-premises requires you toohave hello relevant on-premises license keys.</span></span> <span data-ttu-id="8e7e4-129">建立 VM 之後即無法加入或安裝 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="8e7e4-129">You cannot include or install SQL Server after creating a VM.</span></span> <span data-ttu-id="8e7e4-130">您也必須提供根據已核准的 SQL 影像從 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="8e7e4-130">You must also base your offer on an approved SQL image from hello Azure portal.</span></span> <span data-ttu-id="8e7e4-131">如果您決定 toodevelop 內部，您必須不同於您在開發 hello 雲端中執行一些步驟。</span><span class="sxs-lookup"><span data-stu-id="8e7e4-131">If you decide toodevelop on-premises, you must perform some steps differently than if you were developing in hello cloud.</span></span> <span data-ttu-id="8e7e4-132">您可以在 [建立內部部署 VM 映像](marketplace-publishing-vm-image-creation-on-premise.md)找到相關資訊。</span><span class="sxs-lookup"><span data-stu-id="8e7e4-132">You can find relevant information in [Create an on-premises VM image](marketplace-publishing-vm-image-creation-on-premise.md).</span></span>

[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
