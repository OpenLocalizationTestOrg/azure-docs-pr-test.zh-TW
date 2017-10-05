---
title: "使用適用於 IntelliJ 的 Azure Explorer 來管理儲存體帳戶 | Microsoft Docs"
description: "了解如何使用適用於 IntelliJ 的 Azure 工具組來管理 Azure 儲存體帳戶。"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: a1b56cc2751fc43a1ad6917eca77eec460f26694
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-storage-accounts-by-using-the-azure-explorer-for-intellij"></a><span data-ttu-id="f85a6-103">使用適用於 IntelliJ 的 Azure Explorer 來管理儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="f85a6-103">Manage storage accounts by using the Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="f85a6-104">Azure Explorer 是適用於 IntelliJ 的 Azure 工具組一部分，可為 Java 開發人員提供易於使用的解決方案，從 IntelliJ 整合式開發環境 (IDE) 內管理其 Azure 帳戶中的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f85a6-104">The Azure Explorer, which is part of the Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside the IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-intellij"></a><span data-ttu-id="f85a6-105">在 IntelliJ 中建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="f85a6-105">Create a storage account in IntelliJ</span></span>

<span data-ttu-id="f85a6-106">若要使用 Azure Explorer 來建立儲存體帳戶，請執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="f85a6-106">To create a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="f85a6-107">使用 [Azure Toolkit for Eclipse 的登入指示]來登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f85a6-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for Eclipse].</span></span> 

2. <span data-ttu-id="f85a6-108">在 [Azure Explorer] 檢視中，展開 [Azure] 節點，以滑鼠右鍵按一下 [儲存體帳戶]，然後按一下 [建立儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="f85a6-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![[建立儲存體帳戶] 命令][CS01]

3. <span data-ttu-id="f85a6-110">在 [建立儲存體帳戶] 對話方塊中，指定下列選項：</span><span class="sxs-lookup"><span data-stu-id="f85a6-110">In the **Create Storage Account** dialog box, specify the following options:</span></span>

   ![[新建儲存體帳戶] 對話方塊][CS02]

   * <span data-ttu-id="f85a6-112">**名稱**：指定新儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="f85a6-112">**Name**: Specifies the name for the new storage account.</span></span>

   * <span data-ttu-id="f85a6-113">**帳戶種類**︰指定要建立的儲存體帳戶類型 (例如「Blob 儲存體」)。</span><span class="sxs-lookup"><span data-stu-id="f85a6-113">**Account kind**: Specifies the type of storage account to create (for example, "Blob storage").</span></span> <span data-ttu-id="f85a6-114">如需詳細資訊，請參閱[關於 Azure 儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="f85a6-114">For more information, see [About Azure storage accounts].</span></span> 

   * <span data-ttu-id="f85a6-115">**效能**︰從選取的發行者指定要使用的儲存體帳戶供應項目 (例如「進階」)。</span><span class="sxs-lookup"><span data-stu-id="f85a6-115">**Performance**: Specifies which storage account offering to use from the selected publisher (for example, "Premium").</span></span> <span data-ttu-id="f85a6-116">如需詳細資訊，請參閱 [Azure 儲存體延展性和效能目標]。</span><span class="sxs-lookup"><span data-stu-id="f85a6-116">For more information, see [Azure storage scalability and performance targets].</span></span> 

   * <span data-ttu-id="f85a6-117">**複寫**︰指定儲存體帳戶的複寫 (例如「區域備援」)。</span><span class="sxs-lookup"><span data-stu-id="f85a6-117">**Replication**: Specifies the replication for the storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="f85a6-118">如需詳細資訊，請參閱 [Azure 儲存體複寫]。</span><span class="sxs-lookup"><span data-stu-id="f85a6-118">For more information, see [Azure storage replication].</span></span> 

   * <span data-ttu-id="f85a6-119">**訂用帳戶**：指定您要用於新儲存體帳戶的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f85a6-119">**Subscription**: Specifies the Azure subscription that you want to use for the new storage account.</span></span>

   * <span data-ttu-id="f85a6-120">**位置**︰指定要建立儲存體帳戶的位置 (例如「美國西部」)。</span><span class="sxs-lookup"><span data-stu-id="f85a6-120">**Location**: Specifies the location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="f85a6-121">**資源群組**︰指定虛擬機器的資源群組。</span><span class="sxs-lookup"><span data-stu-id="f85a6-121">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="f85a6-122">選取下列其中一個選項：</span><span class="sxs-lookup"><span data-stu-id="f85a6-122">Select one of the following options:</span></span>
      * <span data-ttu-id="f85a6-123">**新建**：指定您想要建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="f85a6-123">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="f85a6-124">**使用現有項目**︰指定您會從 Azure 帳戶相關聯的資源群組清單中進行選擇。</span><span class="sxs-lookup"><span data-stu-id="f85a6-124">**Use existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

4. <span data-ttu-id="f85a6-125">當您指定好上述所有選項時，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="f85a6-125">When you have specified all of the preceding options, click **OK**.</span></span>

## <a name="create-a-storage-container-in-intellij"></a><span data-ttu-id="f85a6-126">在 IntelliJ 中建立儲存體容器</span><span class="sxs-lookup"><span data-stu-id="f85a6-126">Create a storage container in IntelliJ</span></span>

<span data-ttu-id="f85a6-127">若要使用 Azure Explorer 來建立儲存體容器，請執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="f85a6-127">To create a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="f85a6-128">在 [Azure Explorer] 檢視中，以滑鼠右鍵按一下您要在其中建立容器的儲存體帳戶，然後按一下 [建立 Blob 容器]。</span><span class="sxs-lookup"><span data-stu-id="f85a6-128">In the Azure Explorer view, right-click the storage account where you want to create a container, and then click **Create blob container**.</span></span>

   ![[建立 Blob 容器] 命令][CC01]

2. <span data-ttu-id="f85a6-130">在 [建立 Blob 容器] 對話方塊中指定容器名稱，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="f85a6-130">In the **Create blob container** dialog box, specify the name for your container, and then click **OK**.</span></span> <span data-ttu-id="f85a6-131">如需為儲存體容器命名的詳細資訊，請參閱[命名和參考容器、Blob 及中繼資料]。</span><span class="sxs-lookup"><span data-stu-id="f85a6-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![[建立儲存體容器] 對話方塊][CC02]

## <a name="delete-a-storage-container-in-intellij"></a><span data-ttu-id="f85a6-133">在 IntelliJ 中刪除儲存體容器</span><span class="sxs-lookup"><span data-stu-id="f85a6-133">Delete a storage container in IntelliJ</span></span>

<span data-ttu-id="f85a6-134">若要使用 Azure Explorer 來刪除儲存體容器，請執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="f85a6-134">To delete a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="f85a6-135">在 [Azure Explorer] 檢視中，以滑鼠右鍵按一下儲存體容器，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="f85a6-135">In the Azure Explorer view, right-click the storage container, and then click **Delete**.</span></span>

   ![[刪除儲存體容器] 命令][DC01]

2. <span data-ttu-id="f85a6-137">在確認視窗中，按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="f85a6-137">In the confirmation window, click **Yes**.</span></span>

   ![刪除儲存體容器的確認視窗][DC02]

## <a name="delete-a-storage-account-in-intellij"></a><span data-ttu-id="f85a6-139">在 IntelliJ 中刪除儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="f85a6-139">Delete a storage account in IntelliJ</span></span>

<span data-ttu-id="f85a6-140">若要使用 Azure Explorer 來刪除儲存體帳戶，請執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="f85a6-140">To delete a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="f85a6-141">在 [Azure Explorer] 檢視中，以滑鼠右鍵按一下儲存體帳戶，然後選取 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="f85a6-141">In the **Azure Explorer** view, right-click the storage account, and then select **Delete**.</span></span>

   ![[刪除] 儲存體帳戶功能表][DS01]

2. <span data-ttu-id="f85a6-143">在確認視窗中，按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="f85a6-143">In the confirmation window, click **Yes**.</span></span>

   ![刪除儲存體帳戶的確認視窗][DS02]

## <a name="next-steps"></a><span data-ttu-id="f85a6-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f85a6-145">Next steps</span></span>
<span data-ttu-id="f85a6-146">如需 Azure 儲存體帳戶、大小與定價的詳細資訊，請參閱下列資源︰</span><span class="sxs-lookup"><span data-stu-id="f85a6-146">For more information about Azure storage accounts, sizes, and pricing, see the following resources:</span></span>

* <span data-ttu-id="f85a6-147">[Microsoft Azure 儲存體簡介]</span><span class="sxs-lookup"><span data-stu-id="f85a6-147">[Introduction to Microsoft Azure Storage]</span></span>
* <span data-ttu-id="f85a6-148">[關於 Azure 儲存體帳戶]</span><span class="sxs-lookup"><span data-stu-id="f85a6-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="f85a6-149">Azure 儲存體帳戶大小</span><span class="sxs-lookup"><span data-stu-id="f85a6-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="f85a6-150">[Azure 中的 Windows 儲存體帳戶大小]</span><span class="sxs-lookup"><span data-stu-id="f85a6-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="f85a6-151">[Azure 中的 Linux 儲存體帳戶大小]</span><span class="sxs-lookup"><span data-stu-id="f85a6-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="f85a6-152">Azure 儲存體帳戶定價</span><span class="sxs-lookup"><span data-stu-id="f85a6-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="f85a6-153">[Windows 儲存體帳戶定價]</span><span class="sxs-lookup"><span data-stu-id="f85a6-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="f85a6-154">[Linux 儲存體帳戶定價]</span><span class="sxs-lookup"><span data-stu-id="f85a6-154">[Linux storage-account pricing]</span></span>

<span data-ttu-id="f85a6-155">如需適用於 Java IDE 的 Azure 套件組的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="f85a6-155">For more information about Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="f85a6-156">[適用於 Eclipse 的 Azure 工具組]</span><span class="sxs-lookup"><span data-stu-id="f85a6-156">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="f85a6-157">[Azure Toolkit for Eclipse 的新功能]</span><span class="sxs-lookup"><span data-stu-id="f85a6-157">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="f85a6-158">[安裝 Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f85a6-158">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="f85a6-159">[Azure Toolkit for Eclipse 的登入指示]</span><span class="sxs-lookup"><span data-stu-id="f85a6-159">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="f85a6-160">[在 Eclipse 中建立 Azure Hello World Web 應用程式]</span><span class="sxs-lookup"><span data-stu-id="f85a6-160">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="f85a6-161">[Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="f85a6-161">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f85a6-162">[適用於 IntelliJ 的 Azure 工具組新增功能]</span><span class="sxs-lookup"><span data-stu-id="f85a6-162">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f85a6-163">[安裝 Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="f85a6-163">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f85a6-164">[適用於 IntelliJ 的 Azure 工具組登入指示]</span><span class="sxs-lookup"><span data-stu-id="f85a6-164">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f85a6-165">[在 IntelliJ 中建立 Azure Hello World Web 應用程式]</span><span class="sxs-lookup"><span data-stu-id="f85a6-165">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="f85a6-166">如需有關使用 Azure 搭配 Java 的詳細資訊，請參閱 [Azure Java 開發人員中心]和[適用於 Visual Studio Team Services 的 Java 工具]。</span><span class="sxs-lookup"><span data-stu-id="f85a6-166">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="f85a6-167">[適用於 Eclipse 的 Azure 工具組]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="f85a6-167">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="f85a6-168">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="f85a6-168">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="f85a6-169">[在 Eclipse 中建立 Azure Hello World Web 應用程式]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="f85a6-169">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="f85a6-170">[在 IntelliJ 中建立 Azure Hello World Web 應用程式]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="f85a6-170">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="f85a6-171">[安裝 Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="f85a6-171">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="f85a6-172">[安裝 Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="f85a6-172">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="f85a6-173">[Azure Toolkit for Eclipse 的登入指示]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="f85a6-173">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="f85a6-174">[適用於 IntelliJ 的 Azure 工具組登入指示]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="f85a6-174">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="f85a6-175">[Azure Toolkit for Eclipse 的新功能]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="f85a6-175">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="f85a6-176">[適用於 IntelliJ 的 Azure 工具組新增功能]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="f85a6-176">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="f85a6-177">[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="f85a6-177">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="f85a6-178">[適用於 Visual Studio Team Services 的 Java 工具]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="f85a6-178">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="f85a6-179">[Microsoft Azure 儲存體簡介]: /azure/storage/storage-introduction</span><span class="sxs-lookup"><span data-stu-id="f85a6-179">[Introduction to Microsoft Azure Storage]: /azure/storage/storage-introduction</span></span>
<span data-ttu-id="f85a6-180">[關於 Azure 儲存體帳戶]: /azure/storage/storage-create-storage-account</span><span class="sxs-lookup"><span data-stu-id="f85a6-180">[About Azure storage accounts]: /azure/storage/storage-create-storage-account</span></span>
<span data-ttu-id="f85a6-181">[Azure 儲存體複寫]: /azure/storage/storage-redundancy</span><span class="sxs-lookup"><span data-stu-id="f85a6-181">[Azure storage replication]: /azure/storage/storage-redundancy</span></span>
<span data-ttu-id="f85a6-182">[Azure 儲存體延展性和效能目標]: /azure/storage/storage-scalability-targets</span><span class="sxs-lookup"><span data-stu-id="f85a6-182">[Azure storage scalability and Performance Targets]: /azure/storage/storage-scalability-targets</span></span>
<span data-ttu-id="f85a6-183">[命名和參考容器、Blob 及中繼資料]: http://go.microsoft.com/fwlink/?LinkId=255555</span><span class="sxs-lookup"><span data-stu-id="f85a6-183">[Naming and referencing containers, blobs, and metadata]: http://go.microsoft.com/fwlink/?LinkId=255555</span></span>

<span data-ttu-id="f85a6-184">[Azure 中的 Windows 儲存體帳戶大小]: /azure/virtual-machines/virtual-machines-windows-sizes</span><span class="sxs-lookup"><span data-stu-id="f85a6-184">[Sizes for Windows storage accounts in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span></span>
<span data-ttu-id="f85a6-185">[Azure 中的 Linux 儲存體帳戶大小]: /azure/virtual-machines/virtual-machines-linux-sizes</span><span class="sxs-lookup"><span data-stu-id="f85a6-185">[Sizes for Linux storage accounts in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span></span>
<span data-ttu-id="f85a6-186">[Windows 儲存體帳戶定價]: /pricing/details/virtual-machines/windows/</span><span class="sxs-lookup"><span data-stu-id="f85a6-186">[Windows storage-account pricing]: /pricing/details/virtual-machines/windows/</span></span>
<span data-ttu-id="f85a6-187">[Linux 儲存體帳戶定價]: /pricing/details/virtual-machines/linux/</span><span class="sxs-lookup"><span data-stu-id="f85a6-187">[Linux storage-account pricing]: /pricing/details/virtual-machines/linux/</span></span>

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC02.png
