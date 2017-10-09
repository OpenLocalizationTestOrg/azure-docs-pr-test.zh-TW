---
title: "aaaManage 虛擬機器使用 IntelliJ hello Azure 總管 |Microsoft 文件"
description: "了解如何 toomanage Azure 虛擬機器使用 hello Azure 總管 IntelliJ。"
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
ms.openlocfilehash: a73dd4f73b311dd3413f6712e3b76c36ee464de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-intellij"></a><span data-ttu-id="02029-103">管理虛擬機器使用 IntelliJ hello Azure 總管</span><span class="sxs-lookup"><span data-stu-id="02029-103">Manage virtual machines by using hello Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="02029-104">hello Azure 總管 中，這是 hello Azure Toolkit for IntelliJ 的一部分，提供 Java 開發人員容易使用的解決方案來管理從其 Azure 帳戶中的虛擬機器 hello IntelliJ 整合式的開發環境 (IDE) 內。</span><span class="sxs-lookup"><span data-stu-id="02029-104">hello Azure Explorer, which is part of hello Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside hello IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a><span data-ttu-id="02029-105">在 IntelliJ 中建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="02029-105">Create a virtual machine in IntelliJ</span></span>

<span data-ttu-id="02029-106">請勿 hello toocreate 使用 hello Azure 總管 中，虛擬機器，遵循：</span><span class="sxs-lookup"><span data-stu-id="02029-106">toocreate a virtual machine by using hello Azure Explorer, do hello following:</span></span> 

1. <span data-ttu-id="02029-107">登入 tooyour Azure 帳戶，使用中 hello hello 步驟[登入的指示 hello Azure Toolkit for IntelliJ]發行項。</span><span class="sxs-lookup"><span data-stu-id="02029-107">Sign in tooyour Azure account by using hello steps in hello [Sign-in instructions for hello Azure Toolkit for IntelliJ] article.</span></span>

2. <span data-ttu-id="02029-108">在 hello **Azure 總管**檢視中，展開 hello **Azure**  節點，以滑鼠右鍵按一下**虛擬機器**，然後按一下**建立 VM**。</span><span class="sxs-lookup"><span data-stu-id="02029-108">In hello **Azure Explorer** view, expand hello **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span> 

   <span data-ttu-id="02029-109">![hello 建立 VM 命令][CR01]</span><span class="sxs-lookup"><span data-stu-id="02029-109">![hello Create VM command][CR01]</span></span>  
    <span data-ttu-id="02029-110">hello**建立新的虛擬機器**精靈 隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="02029-110">hello **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="02029-111">在 hello**選擇訂用帳戶**視窗中，選取您的訂閱，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="02029-111">In hello **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span> 

   ![hello 選擇訂用帳戶視窗][CR02]

4. <span data-ttu-id="02029-113">在 hello**選取虛擬機器映像**視窗中，輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="02029-113">In hello **Select a Virtual Machine Image** window, enter hello following information:</span></span>

   * <span data-ttu-id="02029-114">**位置**︰指定要建立虛擬機器的位置 (例如「美國西部」)。</span><span class="sxs-lookup"><span data-stu-id="02029-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span> 

   * <span data-ttu-id="02029-115">**建議的映像**︰指定您會從常用映像的簡短清單中選擇映像。</span><span class="sxs-lookup"><span data-stu-id="02029-115">**Recommended image**: Specifies that you will choose an image from an abbreviated list of commonly used images.</span></span>

   * <span data-ttu-id="02029-116">**自訂映像**： 指定您會藉由提供下列資訊的 hello 選擇自訂映像：</span><span class="sxs-lookup"><span data-stu-id="02029-116">**Custom image**: Specifies that you will choose a custom image by providing hello following information:</span></span>

      * <span data-ttu-id="02029-117">**發行者**： 指定建立 hello 映像，您將使用您的虛擬機器的 hello 發行者 (例如， *Microsoft*)。</span><span class="sxs-lookup"><span data-stu-id="02029-117">**Publisher**: Specifies hello publisher that created hello image that you will use for your virtual machine (for example, *Microsoft*).</span></span>

      * <span data-ttu-id="02029-118">**提供**： 指定從 hello 選取 「 發行者 」 提供 toouse hello 虛擬機器 (例如， *JDK*)。</span><span class="sxs-lookup"><span data-stu-id="02029-118">**Offer**: Specifies hello virtual machine offering toouse from hello selected publisher (for example, *JDK*).</span></span>

      * <span data-ttu-id="02029-119">**Sku**： 指定 hello stockkeeping 單位 (SKU) toouse 從 hello 選供應項目 (例如， *JDK_8*)。</span><span class="sxs-lookup"><span data-stu-id="02029-119">**Sku**: Specifies hello stockkeeping unit (SKU) toouse from hello selected offering (for example, *JDK_8*).</span></span>

      * <span data-ttu-id="02029-120">**版本 #**： 指定哪個版本的 hello 選取 SKU toouse。</span><span class="sxs-lookup"><span data-stu-id="02029-120">**Version #**: Specifies which version of hello selected SKU toouse.</span></span>

   ![選擇虛擬機器映像期間 hello][CR03]

5. <span data-ttu-id="02029-122">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="02029-122">Click **Next**.</span></span> 

6. <span data-ttu-id="02029-123">在 hello**虛擬機器基本設定**視窗中，輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="02029-123">In hello **Virtual Machine Basic Settings** window, enter hello following information:</span></span>

   * <span data-ttu-id="02029-124">**虛擬機器名稱**： 指定新的虛擬機器，必須以字母開頭且只能包含字母、 數字和連字號 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="02029-124">**Virtual machine name**: Specifies hello name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="02029-125">**大小**： 指定 hello 的核心數目和您的虛擬機器的記憶體 tooallocate。</span><span class="sxs-lookup"><span data-stu-id="02029-125">**Size**: Specifies hello number of cores and memory tooallocate for your virtual machine.</span></span>

   * <span data-ttu-id="02029-126">**使用者名稱**： 指定 hello 系統管理員帳戶 toocreate 來管理您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="02029-126">**User name**: Specifies hello administrator account toocreate for managing your virtual machine.</span></span>

   * <span data-ttu-id="02029-127">**密碼**和**確認**： 指定 hello 系統管理員帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="02029-127">**Password** and **Confirm**: Specifies hello password for your administrator account.</span></span>

   ![hello 虛擬機器基本設定 視窗][CR04]

7. <span data-ttu-id="02029-129">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="02029-129">Click **Next**.</span></span> 

8. <span data-ttu-id="02029-130">在 hello**相關聯的資源**視窗中，輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="02029-130">In hello **Associated Resources** window, enter hello following information:</span></span>

   * <span data-ttu-id="02029-131">**資源群組**： 指定您的虛擬機器的 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="02029-131">**Resource group**: Specifies hello resource group for your virtual machine.</span></span> <span data-ttu-id="02029-132">選取其中一個 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="02029-132">Select one of hello following options:</span></span>
      * <span data-ttu-id="02029-133">**建立新**： 指定您想 toocreate 新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="02029-133">**Create new**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="02029-134">**使用現有**： 指定您想 tooselect 從您的 Azure 帳戶相關聯的資源群組的清單。</span><span class="sxs-lookup"><span data-stu-id="02029-134">**Use existing**: Specifies that you want tooselect from a list of resource groups that are associated with your Azure account.</span></span>

       ![hello 相關聯資源的視窗][CR07]

   * <span data-ttu-id="02029-136">**儲存體帳戶**： 指定 hello 儲存體帳戶 toouse 來儲存您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="02029-136">**Storage account**: Specifies hello storage account toouse for storing your virtual machine.</span></span> <span data-ttu-id="02029-137">您可以選擇現有儲存體帳戶或建立新的帳戶。</span><span class="sxs-lookup"><span data-stu-id="02029-137">You can choose an existing storage account or create a new account.</span></span> <span data-ttu-id="02029-138">如果您選擇**新建**，會出現下列對話方塊中的 hello:</span><span class="sxs-lookup"><span data-stu-id="02029-138">If you choose **Create New**, hello following dialog box appears:</span></span>

      ![hello 建立儲存體帳戶對話方塊][CR05]

   * <span data-ttu-id="02029-140">**虛擬網路**和**子網路**： 指定 hello 虛擬網路與虛擬機器會連接到的子網路。</span><span class="sxs-lookup"><span data-stu-id="02029-140">**Virtual Network** and **Subnet**: Specifies hello virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="02029-141">您可以使用現有的網路和子網路，也可以建立新的網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="02029-141">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="02029-142">如果您選取**建立新**，會出現下列對話方塊中的 hello:</span><span class="sxs-lookup"><span data-stu-id="02029-142">If you select **Create new**, hello following dialog box appears:</span></span>

      ![hello 建立虛擬網路 對話方塊][CR06]

   * <span data-ttu-id="02029-144">**公用 IP 位址**︰指定虛擬機器的對外 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="02029-144">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="02029-145">您可以選擇 toocreate 新的 IP 位址，或者如果您的虛擬機器不會有公用 IP 位址，您可以選取**（無）**。</span><span class="sxs-lookup"><span data-stu-id="02029-145">You can choose toocreate a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span> 

   * <span data-ttu-id="02029-146">**網路安全性群組**︰為虛擬機器指定選用的網路防火牆。</span><span class="sxs-lookup"><span data-stu-id="02029-146">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="02029-147">您可以選取現有防火牆，但如果虛擬機器不會使用網路防火牆，您也可以選取 [(無)]。</span><span class="sxs-lookup"><span data-stu-id="02029-147">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span> 

   * <span data-ttu-id="02029-148">**可用性設定組**︰指定虛擬機器可以加入的選用可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="02029-148">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="02029-149">您可以選取現有的可用性設定組，建立新的可用性設定組或，如果您的虛擬機器將不屬於 tooan 可用性設定組中，選取**（無）**。</span><span class="sxs-lookup"><span data-stu-id="02029-149">You can select an existing availability set, create a new availability set or, if your virtual machine will not belong tooan availability set, select **(None)**.</span></span>

9. <span data-ttu-id="02029-150">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="02029-150">Click **Finish**.</span></span>  
    <span data-ttu-id="02029-151">新的虛擬機器會出現在 hello Azure 總管工具視窗。</span><span class="sxs-lookup"><span data-stu-id="02029-151">Your new virtual machine appears in hello Azure Explorer tool window.</span></span> 

   ![Hello Azure 總管檢視中的新虛擬機器][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a><span data-ttu-id="02029-153">在 IntelliJ 中重新啟動虛擬機器</span><span class="sxs-lookup"><span data-stu-id="02029-153">Restart a virtual machine in IntelliJ</span></span>

<span data-ttu-id="02029-154">請勿 hello toorestart 利用 hello Azure 總管 IntelliJ，虛擬機器，遵循：</span><span class="sxs-lookup"><span data-stu-id="02029-154">toorestart a virtual machine by using hello Azure Explorer in IntelliJ, do hello following:</span></span>

1. <span data-ttu-id="02029-155">在 hello **Azure 總管**檢視、 hello 虛擬機器，以滑鼠右鍵按一下，然後選取**重新啟動**。</span><span class="sxs-lookup"><span data-stu-id="02029-155">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Restart**.</span></span>

   ![hello 虛擬機器重新啟動命令][RE01]

2. <span data-ttu-id="02029-157">在 hello 確認視窗中，按一下 **是**。</span><span class="sxs-lookup"><span data-stu-id="02029-157">In hello confirmation window, click **Yes**.</span></span> 

   ![hello 重新啟動虛擬機器確認視窗][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a><span data-ttu-id="02029-159">在 IntelliJ 中將虛擬機器關機</span><span class="sxs-lookup"><span data-stu-id="02029-159">Shut down a virtual machine in IntelliJ</span></span>

<span data-ttu-id="02029-160">關閉執行中虛擬機器中 IntelliJ，使用 hello Azure 總管 tooshut hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="02029-160">tooshut down a running virtual machine by using hello Azure Explorer in IntelliJ, do hello following:</span></span>

1. <span data-ttu-id="02029-161">在 hello **Azure 總管**檢視、 hello 虛擬機器，以滑鼠右鍵按一下，然後選取**關機**。</span><span class="sxs-lookup"><span data-stu-id="02029-161">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Shutdown**.</span></span>

   ![hello 虛擬機器關機命令][SH01]

2. <span data-ttu-id="02029-163">在 hello 確認視窗中，按一下 **是**。</span><span class="sxs-lookup"><span data-stu-id="02029-163">In hello confirmation window, click **Yes**.</span></span> 

   ![關閉虛擬機器確認視窗中的 hello][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a><span data-ttu-id="02029-165">在 IntelliJ 中刪除虛擬機器</span><span class="sxs-lookup"><span data-stu-id="02029-165">Delete a virtual machine in IntelliJ</span></span>

<span data-ttu-id="02029-166">請勿 hello toodelete 利用 hello Azure 總管 IntelliJ，虛擬機器，遵循：</span><span class="sxs-lookup"><span data-stu-id="02029-166">toodelete a virtual machine by using hello Azure Explorer in IntelliJ, do hello following:</span></span>

1. <span data-ttu-id="02029-167">在 hello **Azure 總管**檢視、 hello 虛擬機器，以滑鼠右鍵按一下，然後選取**刪除**。</span><span class="sxs-lookup"><span data-stu-id="02029-167">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Delete**.</span></span>

   ![hello 虛擬機器的 Delete 命令][DE01]

2. <span data-ttu-id="02029-169">在 hello 確認視窗中，按一下 **是**。</span><span class="sxs-lookup"><span data-stu-id="02029-169">In hello confirmation window, click **Yes**.</span></span> 

   ![hello 刪除虛擬機器確認視窗][DE02]

## <a name="next-steps"></a><span data-ttu-id="02029-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="02029-171">Next steps</span></span>
<span data-ttu-id="02029-172">如需 Azure 的虛擬機器大小和定價的詳細資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="02029-172">For more information about Azure virtual-machine sizes and pricing, see hello following resources:</span></span>

* <span data-ttu-id="02029-173">Azure 虛擬機器大小</span><span class="sxs-lookup"><span data-stu-id="02029-173">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="02029-174">[Azure 中的 Windows 虛擬機器大小]</span><span class="sxs-lookup"><span data-stu-id="02029-174">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="02029-175">[Azure 中的 Linux 虛擬機器大小]</span><span class="sxs-lookup"><span data-stu-id="02029-175">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="02029-176">Azure 虛擬機器定價</span><span class="sxs-lookup"><span data-stu-id="02029-176">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="02029-177">[Windows 虛擬機器定價]</span><span class="sxs-lookup"><span data-stu-id="02029-177">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="02029-178">[Linux 虛擬機器定價]</span><span class="sxs-lookup"><span data-stu-id="02029-178">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="02029-179">針對 Java Ide hello Azure 工具套件的相關資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="02029-179">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="02029-180">[適用於 Eclipse 的 Azure 工具組]</span><span class="sxs-lookup"><span data-stu-id="02029-180">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="02029-181">[在 hello Azure Toolkit for Eclipse 中最新消息]</span><span class="sxs-lookup"><span data-stu-id="02029-181">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="02029-182">[安裝 Azure Toolkit for Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="02029-182">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="02029-183">[登入指示 hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="02029-183">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="02029-184">[在 Eclipse 中建立 Azure Hello World Web 應用程式]</span><span class="sxs-lookup"><span data-stu-id="02029-184">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="02029-185">[Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="02029-185">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="02029-186">[在 hello Azure Toolkit for IntelliJ 最新消息]</span><span class="sxs-lookup"><span data-stu-id="02029-186">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="02029-187">[安裝 hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="02029-187">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="02029-188">[登入的指示 hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="02029-188">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="02029-189">[在 IntelliJ 中建立 Azure Hello World Web 應用程式]</span><span class="sxs-lookup"><span data-stu-id="02029-189">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="02029-190">如需有關使用 Azure 搭配 Java 的詳細資訊，請參閱 [Azure Java 開發人員中心]和[適用於 Visual Studio Team Services 的 Java 工具]。</span><span class="sxs-lookup"><span data-stu-id="02029-190">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

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

[Azure 中的 Windows 虛擬機器大小]: /azure/virtual-machines/virtual-machines-windows-sizes
[Azure 中的 Linux 虛擬機器大小]: /azure/virtual-machines/virtual-machines-linux-sizes
[Windows 虛擬機器定價]: /pricing/details/virtual-machines/windows/
[Linux 虛擬機器定價]: /pricing/details/virtual-machines/linux/


<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR08.png
