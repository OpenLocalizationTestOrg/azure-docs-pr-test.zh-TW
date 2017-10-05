---
title: "建立 Azure Marketplace 虛擬機器映像的技術性必要條件 | Microsoft Docs"
description: "了解建立和部署虛擬機器映像到 Azure Marketplace 供他人購買的要求。"
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
ms.openlocfilehash: af3e2ad623d8d7bfafe676411f9ae3fbee78aab8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="technical-prerequisites-for-creating-a-virtual-machine-image-for-the-azure-marketplace"></a><span data-ttu-id="97060-103">建立 Azure Marketplace 虛擬機器映像的技術性必要條件</span><span class="sxs-lookup"><span data-stu-id="97060-103">Technical prerequisites for creating a virtual machine image for the Azure Marketplace</span></span>
<span data-ttu-id="97060-104">開始之前，請先徹底閱讀程序，並且了解每個步驟執行的位置及原因。</span><span class="sxs-lookup"><span data-stu-id="97060-104">Read the process thoroughly before beginning and understand where and why each step is performed.</span></span> <span data-ttu-id="97060-105">在供應項目建立程序之前，您應該盡可能準備您的公司資訊和其他資料、下載必要的工具，和/或建立技術元件。</span><span class="sxs-lookup"><span data-stu-id="97060-105">As much as possible, you should prepare your company information and other data, download necessary tools, and/or create technical components before beginning the offer creation process.</span></span> <span data-ttu-id="97060-106">檢閱本文之後，您會更清楚這些項目。</span><span class="sxs-lookup"><span data-stu-id="97060-106">These items should be clear from reviewing this article.</span></span>  

## <a name="download-needed-tools--applications"></a><span data-ttu-id="97060-107">下載需要的工具和應用程式</span><span class="sxs-lookup"><span data-stu-id="97060-107">Download needed tools & applications</span></span>
<span data-ttu-id="97060-108">開始程序之前，您應該先準備好下列項目：</span><span class="sxs-lookup"><span data-stu-id="97060-108">You should have the following items ready before beginning the process:</span></span>

* <span data-ttu-id="97060-109">視您的目標作業系統而定，從 [Azure 下載](https://azure.microsoft.com/downloads/)頁面安裝 [Azure PowerShell Cmdlet](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) 或 [Linux 命令列介面工具](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="97060-109">Depending on which operating system you are targeting, install the [Azure PowerShell cmdlets](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) or [Linux command-line interface tool](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) from the [Azure Downloads](https://azure.microsoft.com/downloads/) page.</span></span>
* <span data-ttu-id="97060-110">從 CodePlex 安裝 Azure 儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="97060-110">Install Azure Storage Explorer from CodePlex.</span></span>
* <span data-ttu-id="97060-111">下載並安裝適用於 Azure 認證的認證測試工具：</span><span class="sxs-lookup"><span data-stu-id="97060-111">Download and install the Certification Test Tool for Azure Certified:</span></span>
  * <span data-ttu-id="97060-112">[http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913)。</span><span class="sxs-lookup"><span data-stu-id="97060-112">[http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913).</span></span> <span data-ttu-id="97060-113">您需要 Windows 架構的電腦才能執行認證工具。</span><span class="sxs-lookup"><span data-stu-id="97060-113">You need a Windows-based computer to run the certification tool.</span></span> <span data-ttu-id="97060-114">如果您沒有 Windows 電腦，可以在 Azure 中使用 Windows 架構的 VM 執行工具。</span><span class="sxs-lookup"><span data-stu-id="97060-114">If you do not have a Windows-based computer available, you can run the tool using a Windows-based VM in Azure.</span></span>

## <a name="platforms-supported"></a><span data-ttu-id="97060-115">支援的平台</span><span class="sxs-lookup"><span data-stu-id="97060-115">Platforms supported</span></span>
<span data-ttu-id="97060-116">您可以在 Windows 或 Linux 上開發 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="97060-116">You can develop Azure-based VMs on Windows or Linux.</span></span> <span data-ttu-id="97060-117">發佈程序的一些項目—例如建立與 Azure 相容的虛擬硬碟 (VHD)—會根據使用的作業系統而使用不同的工具和步驟。</span><span class="sxs-lookup"><span data-stu-id="97060-117">Some elements of the publishing process--such as creating an Azure-compatible virtual hard disk (VHD)--use different tools and steps depending on which operating system you are using:</span></span>  

* <span data-ttu-id="97060-118">如果您使用 Linux，請參閱 [虛擬機器映像發佈指南](marketplace-publishing-vm-image-creation.md)的＜建立與 Azure 相容的 VHD (以 Linux 為基礎)＞一節。</span><span class="sxs-lookup"><span data-stu-id="97060-118">If you are using Linux, refer to the “Create an Azure-compatible VHD (Linux-based)” section of the [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md).</span></span>
* <span data-ttu-id="97060-119">如果您使用 Windows，請參閱 [虛擬機器映像發佈指南](marketplace-publishing-vm-image-creation.md)的＜建立與 Azure 相容的 VHD (以 Windows 為基礎)＞一節。</span><span class="sxs-lookup"><span data-stu-id="97060-119">If you are using Windows, refer to the “Create an Azure-compatible VHD (Windows-based)” section of the [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md).</span></span>

> [!NOTE]
> <span data-ttu-id="97060-120">您需要有 Windows 電腦的存取權才能︰</span><span class="sxs-lookup"><span data-stu-id="97060-120">You need access to a Windows-based machine to:</span></span>
> 
> * <span data-ttu-id="97060-121">執行憑證驗證工具。</span><span class="sxs-lookup"><span data-stu-id="97060-121">Run the certification validation tool.</span></span>
> * <span data-ttu-id="97060-122">建立送出 VHD 憑證的 VHD 共用存取簽章 URL。</span><span class="sxs-lookup"><span data-stu-id="97060-122">Create the VHD shared access signature URL for the VHD certification submission.</span></span>
> 
> 

## <a name="develop-your-vhd"></a><span data-ttu-id="97060-123">開發您的 VHD</span><span class="sxs-lookup"><span data-stu-id="97060-123">Develop your VHD</span></span>
<span data-ttu-id="97060-124">您可以在雲端或內部部署中開發 Azure VHD：</span><span class="sxs-lookup"><span data-stu-id="97060-124">You can develop Azure VHDs in the cloud or on-premises:</span></span>

* <span data-ttu-id="97060-125">雲端開發表示所有開發步驟都會在 Azure 的 VHD 上遠端執行。</span><span class="sxs-lookup"><span data-stu-id="97060-125">Cloud-based development means all development steps are performed remotely on a VHD resident on Azure.</span></span>
* <span data-ttu-id="97060-126">內部部署開發則需要使用內部部署基礎結構下載 VHD 和開發。</span><span class="sxs-lookup"><span data-stu-id="97060-126">On-premises development requires downloading a VHD and developing it using on-premises infrastructure.</span></span> <span data-ttu-id="97060-127">雖然可行，但我們不建議您這麼做。</span><span class="sxs-lookup"><span data-stu-id="97060-127">Although this is possible, we do not recommend it.</span></span> <span data-ttu-id="97060-128">請注意，為內部部署的 Windows 或 SQL 開發時，需要有相關的內部部署授權金鑰。</span><span class="sxs-lookup"><span data-stu-id="97060-128">Note that developing for Windows or SQL on-premises requires you to have the relevant on-premises license keys.</span></span> <span data-ttu-id="97060-129">建立 VM 之後即無法加入或安裝 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="97060-129">You cannot include or install SQL Server after creating a VM.</span></span> <span data-ttu-id="97060-130">此外，您必須讓供應項目以 Azure 入口網站中核准的 SQL 映像為基礎。</span><span class="sxs-lookup"><span data-stu-id="97060-130">You must also base your offer on an approved SQL image from the Azure portal.</span></span> <span data-ttu-id="97060-131">如果您決定開發內部部署，必須執行一些不同於在雲端中開發的步驟。</span><span class="sxs-lookup"><span data-stu-id="97060-131">If you decide to develop on-premises, you must perform some steps differently than if you were developing in the cloud.</span></span> <span data-ttu-id="97060-132">您可以在 [建立內部部署 VM 映像](marketplace-publishing-vm-image-creation-on-premise.md)找到相關資訊。</span><span class="sxs-lookup"><span data-stu-id="97060-132">You can find relevant information in [Create an on-premises VM image](marketplace-publishing-vm-image-creation-on-premise.md).</span></span>

[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
