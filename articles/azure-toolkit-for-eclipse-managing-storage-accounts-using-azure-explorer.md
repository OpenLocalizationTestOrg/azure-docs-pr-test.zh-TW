---
title: "aaaManage 儲存體帳戶使用 hello 適用於 Eclipse 的 Azure Explorer |Microsoft 文件"
description: "了解如何 toomanage 您 Azure 儲存體帳戶會利用 hello Azure 總管 for Eclipse。"
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
ms.openlocfilehash: b7ec53e77e3c96d87754b9a658d31e6182121b22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-storage-accounts-by-using-hello-azure-explorer-for-eclipse"></a><span data-ttu-id="da9a4-103">使用適用於 Eclipse 的 hello Azure 總管來管理儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="da9a4-103">Manage storage accounts by using hello Azure Explorer for Eclipse</span></span>

<span data-ttu-id="da9a4-104">hello Azure 總管 中，這是 hello Azure Toolkit for Eclipse 的一部分，Java 開發人員提供方便使用方案管理從其 Azure 帳戶中的儲存體帳戶內 hello Eclipse 整合式的開發環境 (IDE)。</span><span class="sxs-lookup"><span data-stu-id="da9a4-104">hello Azure Explorer, which is part of hello Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside hello Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-eclipse"></a><span data-ttu-id="da9a4-105">在 Eclipse 中建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="da9a4-105">Create a storage account in Eclipse</span></span>

<span data-ttu-id="da9a4-106">toocreate 儲存體帳戶使用 hello Azure 總管 中，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="da9a4-106">toocreate a storage account by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="da9a4-107">使用 hello 登入 Azure 帳戶 tooyour[登入指示 hello Azure Toolkit for Eclipse]。</span><span class="sxs-lookup"><span data-stu-id="da9a4-107">Sign in tooyour Azure account by using hello [Sign-in instructions for hello Azure Toolkit for Eclipse].</span></span>

2. <span data-ttu-id="da9a4-108">在 hello **Azure 總管**檢視中，展開 hello **Azure**  節點，以滑鼠右鍵按一下**儲存體帳戶**，然後按一下**建立儲存體帳戶**.</span><span class="sxs-lookup"><span data-stu-id="da9a4-108">In hello **Azure Explorer** view, expand hello **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![[建立儲存體帳戶] 命令][CS01]

3. <span data-ttu-id="da9a4-110">在 hello**建立儲存體帳戶**對話方塊方塊中，指定下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="da9a4-110">In hello **Create Storage Account** dialog box, specify hello following options:</span></span>

   ![[新建儲存體帳戶] 對話方塊][CS02]

   * <span data-ttu-id="da9a4-112">**名稱**： 指定 hello hello 新儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="da9a4-112">**Name**: Specifies hello name for hello new storage account.</span></span>

   * <span data-ttu-id="da9a4-113">**訂用帳戶**： 指定 hello toouse 需 hello 新儲存體帳戶的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="da9a4-113">**Subscription**: Specifies hello Azure subscription that you want toouse for hello new storage account.</span></span>

   * <span data-ttu-id="da9a4-114">**資源群組**： 指定您的虛擬機器的 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="da9a4-114">**Resource Group**: Specifies hello resource group for your virtual machine.</span></span> <span data-ttu-id="da9a4-115">選取其中一個 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="da9a4-115">Select one of hello following options:</span></span>
      * <span data-ttu-id="da9a4-116">**建立新**： 指定您想 toocreate 新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="da9a4-116">**Create New**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="da9a4-117">**使用現有項目**︰指定您會從 Azure 帳戶相關聯的資源群組清單中進行選擇。</span><span class="sxs-lookup"><span data-stu-id="da9a4-117">**Use Existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

   * <span data-ttu-id="da9a4-118">**區域**： 指定儲存體帳戶 （例如，「 美國西部 」） 的建立位置的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="da9a4-118">**Region**: Specifies hello location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="da9a4-119">**帳戶類型**： 指定 hello 類型的儲存體帳戶 toocreate （例如，"Blob 儲存 」）。</span><span class="sxs-lookup"><span data-stu-id="da9a4-119">**Account kind**: Specifies hello type of storage account toocreate (for example, "Blob storage").</span></span> <span data-ttu-id="da9a4-120">如需詳細資訊，請參閱[關於 Azure 儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="da9a4-120">For more information, see [About Azure storage accounts].</span></span>

   * <span data-ttu-id="da9a4-121">**效能**： 指定提供 toouse 從 hello （例如，「 進階版 」） 的 選取 「 發行者 」 的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="da9a4-121">**Performance**: Specifies which storage account offering toouse from hello selected publisher (for example, "Premium").</span></span> <span data-ttu-id="da9a4-122">如需詳細資訊，請參閱 [Azure 儲存體延展性和效能目標]。</span><span class="sxs-lookup"><span data-stu-id="da9a4-122">For more information, see [Azure storage scalability and performance targets].</span></span>

   * <span data-ttu-id="da9a4-123">**複寫**： 指定 hello 複寫 hello 儲存體帳戶 （例如，「 區域備援 」）。</span><span class="sxs-lookup"><span data-stu-id="da9a4-123">**Replication**: Specifies hello replication for hello storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="da9a4-124">如需詳細資訊，請參閱 [Azure 儲存體複寫]。</span><span class="sxs-lookup"><span data-stu-id="da9a4-124">For more information, see [Azure storage replication].</span></span>

4. <span data-ttu-id="da9a4-125">當您指定了所有 hello 上述選項時，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="da9a4-125">When you have specified all of hello preceding options, click **Create**.</span></span>

## <a name="create-a-storage-container-in-eclipse"></a><span data-ttu-id="da9a4-126">在 Eclipse 中建立儲存體容器</span><span class="sxs-lookup"><span data-stu-id="da9a4-126">Create a storage container in Eclipse</span></span>

<span data-ttu-id="da9a4-127">toocreate 使用 hello Azure 總管 中，儲存體容器 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="da9a4-127">toocreate a storage container by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="da9a4-128">在 hello **Azure 總管**檢視中，以滑鼠右鍵按一下您想 toocreate 容器，然後再按一下 hello 儲存體帳戶**建立 blob 容器**。</span><span class="sxs-lookup"><span data-stu-id="da9a4-128">In hello **Azure Explorer** view, right-click hello storage account where you want toocreate a container, and then click **Create blob container**.</span></span>

   ![[建立 Blob 容器] 命令][CC01]

2. <span data-ttu-id="da9a4-130">在 hello**建立 blob 容器**對話方塊中，指定您的容器，hello 名稱，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="da9a4-130">In hello **Create blob container** dialog box, specify hello name for your container, and then click **OK**.</span></span> <span data-ttu-id="da9a4-131">如需為儲存體容器命名的詳細資訊，請參閱[命名和參考容器、Blob 及中繼資料]。</span><span class="sxs-lookup"><span data-stu-id="da9a4-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![[建立 Blob 容器] 對話方塊][CC02]

## <a name="delete-a-storage-container-in-eclipse"></a><span data-ttu-id="da9a4-133">在 Eclipse 中刪除儲存體容器</span><span class="sxs-lookup"><span data-stu-id="da9a4-133">Delete a storage container in Eclipse</span></span>

<span data-ttu-id="da9a4-134">toodelete 使用 hello Azure 總管 中，儲存體容器 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="da9a4-134">toodelete a storage container by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="da9a4-135">在 hello **Azure 總管**檢視，以滑鼠右鍵按一下 hello 儲存體容器，然後再按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="da9a4-135">In hello **Azure Explorer** view, right-click hello storage container, and then click **Delete**.</span></span>

   ![[刪除儲存體容器] 命令][DC01]

2. <span data-ttu-id="da9a4-137">在 hello 確認視窗中，按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="da9a4-137">In hello confirmation window, click **OK**.</span></span>

   ![刪除儲存體容器的確認視窗][DC02]

## <a name="delete-a-storage-account-in-eclipse"></a><span data-ttu-id="da9a4-139">在 Eclipse 中刪除儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="da9a4-139">Delete a storage account in Eclipse</span></span>

<span data-ttu-id="da9a4-140">toodelete 儲存體帳戶使用 hello Azure 總管 中，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="da9a4-140">toodelete a storage account by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="da9a4-141">在 hello **Azure 總管**檢視，hello 儲存體帳戶，以滑鼠右鍵按一下，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="da9a4-141">In hello **Azure Explorer** view, right-click hello storage account, and then click **Delete**.</span></span>

   ![[刪除儲存體帳戶] 命令][DS01]

2. <span data-ttu-id="da9a4-143">在 hello 確認視窗中，按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="da9a4-143">In hello confirmation window, click **OK**.</span></span>

   ![刪除儲存體帳戶的確認視窗][DS02]

## <a name="next-steps"></a><span data-ttu-id="da9a4-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="da9a4-145">Next steps</span></span>
<span data-ttu-id="da9a4-146">如需 Azure 儲存體帳戶、 大小以及價格的詳細資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="da9a4-146">For more information about Azure storage accounts, sizes, and pricing, see hello following resources:</span></span>

* <span data-ttu-id="da9a4-147">[簡介 tooMicrosoft Azure 儲存體]</span><span class="sxs-lookup"><span data-stu-id="da9a4-147">[Introduction tooMicrosoft Azure Storage]</span></span>
* <span data-ttu-id="da9a4-148">[關於 Azure 儲存體帳戶]</span><span class="sxs-lookup"><span data-stu-id="da9a4-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="da9a4-149">Azure 儲存體帳戶大小</span><span class="sxs-lookup"><span data-stu-id="da9a4-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="da9a4-150">[Azure 中的 Windows 儲存體帳戶大小]</span><span class="sxs-lookup"><span data-stu-id="da9a4-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="da9a4-151">[Azure 中的 Linux 儲存體帳戶大小]</span><span class="sxs-lookup"><span data-stu-id="da9a4-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="da9a4-152">Azure 儲存體帳戶定價</span><span class="sxs-lookup"><span data-stu-id="da9a4-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="da9a4-153">[Windows 儲存體帳戶定價]</span><span class="sxs-lookup"><span data-stu-id="da9a4-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="da9a4-154">[Linux 儲存體帳戶定價]</span><span class="sxs-lookup"><span data-stu-id="da9a4-154">[Linux storage-account pricing]</span></span>

<span data-ttu-id="da9a4-155">Java Ide 的 Azure 工具套件的相關資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="da9a4-155">For more information about Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="da9a4-156">[適用於 Eclipse 的 Azure 工具組]</span><span class="sxs-lookup"><span data-stu-id="da9a4-156">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="da9a4-157">[在 hello Azure Toolkit for Eclipse 中最新消息]</span><span class="sxs-lookup"><span data-stu-id="da9a4-157">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="da9a4-158">[安裝 Azure Toolkit for Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="da9a4-158">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="da9a4-159">[登入指示 hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="da9a4-159">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="da9a4-160">[在 Eclipse 中建立 Azure Hello World Web 應用程式]</span><span class="sxs-lookup"><span data-stu-id="da9a4-160">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="da9a4-161">[Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="da9a4-161">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="da9a4-162">[在 hello Azure Toolkit for IntelliJ 最新消息]</span><span class="sxs-lookup"><span data-stu-id="da9a4-162">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="da9a4-163">[安裝 hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="da9a4-163">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="da9a4-164">[登入的指示 hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="da9a4-164">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="da9a4-165">[在 IntelliJ 中建立 Azure Hello World Web 應用程式]</span><span class="sxs-lookup"><span data-stu-id="da9a4-165">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="da9a4-166">如需有關使用 Azure 搭配 Java 的詳細資訊，請參閱 [Azure Java 開發人員中心]和[適用於 Visual Studio Team Services 的 Java 工具]。</span><span class="sxs-lookup"><span data-stu-id="da9a4-166">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[適用於 Eclipse 的 Azure 工具組]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md
[在 Eclipse 中建立 Azure Hello World Web 應用程式]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[在 IntelliJ 中建立 Azure Hello World Web 應用程式]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[安裝 Azure Toolkit for Eclipse hello]: ./azure-toolkit-for-eclipse-installation.md
[安裝 hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[登入指示 hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[登入的指示 hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[在 hello Azure Toolkit for Eclipse 中最新消息]: ./azure-toolkit-for-eclipse-whats-new.md
[在 hello Azure Toolkit for IntelliJ 最新消息]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/
[適用於 Visual Studio Team Services 的 Java 工具]: https://java.visualstudio.com/

[簡介 tooMicrosoft Azure 儲存體]: /azure/storage/storage-introduction
[關於 Azure 儲存體帳戶]: /azure/storage/storage-create-storage-account
[Azure 儲存體複寫]: /azure/storage/storage-redundancy
[Azure 儲存體延展性和效能目標]: /azure/storage/storage-scalability-targets
[命名和參考容器、Blob 及中繼資料]: http://go.microsoft.com/fwlink/?LinkId=255555

[Azure 中的 Windows 儲存體帳戶大小]: /azure/virtual-machines/virtual-machines-windows-sizes
[Azure 中的 Linux 儲存體帳戶大小]: /azure/virtual-machines/virtual-machines-linux-sizes
[Windows 儲存體帳戶定價]: /pricing/details/virtual-machines/windows/
[Linux 儲存體帳戶定價]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC02.png
