---
title: "使用適用於 IntelliJ 的 Azure Explorer 來管理虛擬機器 | Microsoft Docs"
description: "了解如何使用適用於 IntelliJ 的 Azure 工具組來管理 Azure 虛擬機器。"
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
ms.openlocfilehash: 9197580407b3509fbf9a842e1fee1e6348478c34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-intellij"></a><span data-ttu-id="502ac-103">使用適用於 IntelliJ 的 Azure Explorer 來管理虛擬機器</span><span class="sxs-lookup"><span data-stu-id="502ac-103">Manage virtual machines by using the Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="502ac-104">Azure Explorer 是適用於 IntelliJ 的 Azure 工具組一部分，可為 Java 開發人員提供易於使用的解決方案，從 IntelliJ 整合式開發環境 (IDE) 內管理其 Azure 帳戶中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="502ac-104">The Azure Explorer, which is part of the Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside the IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a><span data-ttu-id="502ac-105">在 IntelliJ 中建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="502ac-105">Create a virtual machine in IntelliJ</span></span>

<span data-ttu-id="502ac-106">若要使用 Azure Explorer 來建立虛擬機器，請執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="502ac-106">To create a virtual machine by using the Azure Explorer, do the following:</span></span> 

1. <span data-ttu-id="502ac-107">使用[適用於 IntelliJ 的 Azure 工具組登入指示]文章中的步驟來登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="502ac-107">Sign in to your Azure account by using the steps in the [Sign-in instructions for the Azure Toolkit for IntelliJ] article.</span></span>

2. <span data-ttu-id="502ac-108">在 [Azure Explorer] 檢視中，展開 [Azure] 節點，以滑鼠右鍵按一下 [虛擬機器]，然後按一下 [建立 VM]。</span><span class="sxs-lookup"><span data-stu-id="502ac-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span> 

   <span data-ttu-id="502ac-109">![建立 VM 命令][CR01]</span><span class="sxs-lookup"><span data-stu-id="502ac-109">![The Create VM command][CR01]</span></span>  
    <span data-ttu-id="502ac-110">[建立新的虛擬機器] 精靈隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="502ac-110">The **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="502ac-111">在 [選擇訂用帳戶] 視窗中選取您的訂用帳戶，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="502ac-111">In the **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span> 

   ![選擇訂用帳戶視窗][CR02]

4. <span data-ttu-id="502ac-113">在 [選取虛擬機器映像] 視窗中，輸入下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="502ac-113">In the **Select a Virtual Machine Image** window, enter the following information:</span></span>

   * <span data-ttu-id="502ac-114">**位置**︰指定要建立虛擬機器的位置 (例如「美國西部」)。</span><span class="sxs-lookup"><span data-stu-id="502ac-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span> 

   * <span data-ttu-id="502ac-115">**建議的映像**︰指定您會從常用映像的簡短清單中選擇映像。</span><span class="sxs-lookup"><span data-stu-id="502ac-115">**Recommended image**: Specifies that you will choose an image from an abbreviated list of commonly used images.</span></span>

   * <span data-ttu-id="502ac-116">**自訂映像**︰指定您會藉由提供下列資訊來選擇自訂映像︰</span><span class="sxs-lookup"><span data-stu-id="502ac-116">**Custom image**: Specifies that you will choose a custom image by providing the following information:</span></span>

      * <span data-ttu-id="502ac-117">**發行者**︰指定要讓虛擬機器使用的映像是由哪個發行者所建立 (例如「Microsoft」)。</span><span class="sxs-lookup"><span data-stu-id="502ac-117">**Publisher**: Specifies the publisher that created the image that you will use for your virtual machine (for example, *Microsoft*).</span></span>

      * <span data-ttu-id="502ac-118">**供應項目**︰從選取的發行者中指定要使用的虛擬機器供應項目 (例如「JDK」)。</span><span class="sxs-lookup"><span data-stu-id="502ac-118">**Offer**: Specifies the virtual machine offering to use from the selected publisher (for example, *JDK*).</span></span>

      * <span data-ttu-id="502ac-119">**SKU**︰從選取的供應項目中指定要使用的 Stockkeeping 單元 (SKU) (例如「JDK_8」)。</span><span class="sxs-lookup"><span data-stu-id="502ac-119">**Sku**: Specifies the stockkeeping unit (SKU) to use from the selected offering (for example, *JDK_8*).</span></span>

      * <span data-ttu-id="502ac-120">**版本 #**︰指定所選 SKU 要使用的版本。</span><span class="sxs-lookup"><span data-stu-id="502ac-120">**Version #**: Specifies which version of the selected SKU to use.</span></span>

   ![選取虛擬機器映像視窗][CR03]

5. <span data-ttu-id="502ac-122">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="502ac-122">Click **Next**.</span></span> 

6. <span data-ttu-id="502ac-123">在 [虛擬機器基本設定] 視窗中，輸入下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="502ac-123">In the **Virtual Machine Basic Settings** window, enter the following information:</span></span>

   * <span data-ttu-id="502ac-124">**虛擬機器名稱**：指定您新虛擬機器的名稱，其必須以字母開頭，且只能包含字母、數字及連字號。</span><span class="sxs-lookup"><span data-stu-id="502ac-124">**Virtual machine name**: Specifies the name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="502ac-125">**大小**︰指定要配置給虛擬機器的核心和記憶體數目。</span><span class="sxs-lookup"><span data-stu-id="502ac-125">**Size**: Specifies the number of cores and memory to allocate for your virtual machine.</span></span>

   * <span data-ttu-id="502ac-126">**使用者名稱**︰指定要管理您的虛擬機器所建立的系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="502ac-126">**User name**: Specifies the administrator account to create for managing your virtual machine.</span></span>

   * <span data-ttu-id="502ac-127">**密碼**和**確認**︰指定您系統管理員帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="502ac-127">**Password** and **Confirm**: Specifies the password for your administrator account.</span></span>

   ![虛擬機器基本設定視窗][CR04]

7. <span data-ttu-id="502ac-129">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="502ac-129">Click **Next**.</span></span> 

8. <span data-ttu-id="502ac-130">在 [相關聯的資源] 視窗中，輸入下列資訊：</span><span class="sxs-lookup"><span data-stu-id="502ac-130">In the **Associated Resources** window, enter the following information:</span></span>

   * <span data-ttu-id="502ac-131">**資源群組**︰指定虛擬機器的資源群組。</span><span class="sxs-lookup"><span data-stu-id="502ac-131">**Resource group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="502ac-132">選取下列其中一個選項：</span><span class="sxs-lookup"><span data-stu-id="502ac-132">Select one of the following options:</span></span>
      * <span data-ttu-id="502ac-133">**新建**：指定您想要建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="502ac-133">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="502ac-134">**使用現有項目**︰指定您要從 Azure 帳戶相關聯的資源群組清單中進行選擇。</span><span class="sxs-lookup"><span data-stu-id="502ac-134">**Use existing**: Specifies that you want to select from a list of resource groups that are associated with your Azure account.</span></span>

       ![[相關聯的資源] 視窗][CR07]

   * <span data-ttu-id="502ac-136">**儲存體帳戶**︰指定要用來儲存虛擬機器的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="502ac-136">**Storage account**: Specifies the storage account to use for storing your virtual machine.</span></span> <span data-ttu-id="502ac-137">您可以選擇現有儲存體帳戶或建立新的帳戶。</span><span class="sxs-lookup"><span data-stu-id="502ac-137">You can choose an existing storage account or create a new account.</span></span> <span data-ttu-id="502ac-138">如果您選擇 [新建]，畫面上會隨即顯示下列對話方塊︰</span><span class="sxs-lookup"><span data-stu-id="502ac-138">If you choose **Create New**, the following dialog box appears:</span></span>

      ![[建立儲存體帳戶] 對話方塊][CR05]

   * <span data-ttu-id="502ac-140">**虛擬網路**和**子網路**︰指定虛擬機器所要連線的虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="502ac-140">**Virtual Network** and **Subnet**: Specifies the virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="502ac-141">您可以使用現有的網路和子網路，也可以建立新的網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="502ac-141">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="502ac-142">如果您選取 [新建]，畫面上會隨即顯示下列對話方塊︰</span><span class="sxs-lookup"><span data-stu-id="502ac-142">If you select **Create new**, the following dialog box appears:</span></span>

      ![[建立虛擬網路] 對話方塊][CR06]

   * <span data-ttu-id="502ac-144">**公用 IP 位址**︰指定虛擬機器的對外 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="502ac-144">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="502ac-145">您可以選擇建立新的 IP 位址，但如果虛擬機器不會有公用 IP 位址，您也可以選取 [(無)]。</span><span class="sxs-lookup"><span data-stu-id="502ac-145">You can choose to create a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span> 

   * <span data-ttu-id="502ac-146">**網路安全性群組**︰為虛擬機器指定選用的網路防火牆。</span><span class="sxs-lookup"><span data-stu-id="502ac-146">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="502ac-147">您可以選取現有防火牆，但如果虛擬機器不會使用網路防火牆，您也可以選取 [(無)]。</span><span class="sxs-lookup"><span data-stu-id="502ac-147">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span> 

   * <span data-ttu-id="502ac-148">**可用性設定組**︰指定虛擬機器可以加入的選用可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="502ac-148">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="502ac-149">您可以選取現有的可用性設定組、建立新的可用性設定組，也可以在虛擬機器不會加入任何可用性設定組時選取 [(無)]。</span><span class="sxs-lookup"><span data-stu-id="502ac-149">You can select an existing availability set, create a new availability set or, if your virtual machine will not belong to an availability set, select **(None)**.</span></span>

9. <span data-ttu-id="502ac-150">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="502ac-150">Click **Finish**.</span></span>  
    <span data-ttu-id="502ac-151">[Azure Explorer] 工具視窗中便會出現新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="502ac-151">Your new virtual machine appears in the Azure Explorer tool window.</span></span> 

   ![[Azure Explorer] 檢視中的新虛擬機器][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a><span data-ttu-id="502ac-153">在 IntelliJ 中重新啟動虛擬機器</span><span class="sxs-lookup"><span data-stu-id="502ac-153">Restart a virtual machine in IntelliJ</span></span>

<span data-ttu-id="502ac-154">若要在 IntelliJ 中使用 Azure Explorer 重新啟動虛擬機器，請執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="502ac-154">To restart a virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="502ac-155">在 [Azure Explorer] 檢視中，以滑鼠右鍵按一下虛擬機器，然後選取 [重新啟動]。</span><span class="sxs-lookup"><span data-stu-id="502ac-155">In the **Azure Explorer** view, right-click the virtual machine, and then select **Restart**.</span></span>

   ![虛擬機器重新啟動命令][RE01]

2. <span data-ttu-id="502ac-157">在確認視窗中，按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="502ac-157">In the confirmation window, click **Yes**.</span></span> 

   ![重新啟動虛擬機器的確認視窗][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a><span data-ttu-id="502ac-159">在 IntelliJ 中將虛擬機器關機</span><span class="sxs-lookup"><span data-stu-id="502ac-159">Shut down a virtual machine in IntelliJ</span></span>

<span data-ttu-id="502ac-160">若要在 IntelliJ 中使用 Azure Explorer 將執行中的虛擬機器關機，請執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="502ac-160">To shut down a running virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="502ac-161">在 [Azure Explorer] 檢視中，以滑鼠右鍵按一下虛擬機器，然後選取 [關機]。</span><span class="sxs-lookup"><span data-stu-id="502ac-161">In the **Azure Explorer** view, right-click the virtual machine, and then select **Shutdown**.</span></span>

   ![虛擬機器關機命令][SH01]

2. <span data-ttu-id="502ac-163">在確認視窗中，按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="502ac-163">In the confirmation window, click **Yes**.</span></span> 

   ![將虛擬機器關機的確認視窗][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a><span data-ttu-id="502ac-165">在 IntelliJ 中刪除虛擬機器</span><span class="sxs-lookup"><span data-stu-id="502ac-165">Delete a virtual machine in IntelliJ</span></span>

<span data-ttu-id="502ac-166">若要在 IntelliJ 中使用 Azure Explorer 刪除虛擬機器，請執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="502ac-166">To delete a virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="502ac-167">在 [Azure Explorer] 檢視中，以滑鼠右鍵按一下虛擬機器，然後選取 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="502ac-167">In the **Azure Explorer** view, right-click the virtual machine, and then select **Delete**.</span></span>

   ![虛擬機器刪除命令][DE01]

2. <span data-ttu-id="502ac-169">在確認視窗中，按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="502ac-169">In the confirmation window, click **Yes**.</span></span> 

   ![刪除虛擬機器的確認視窗][DE02]

## <a name="next-steps"></a><span data-ttu-id="502ac-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="502ac-171">Next steps</span></span>
<span data-ttu-id="502ac-172">如需 Azure 虛擬機器大小與定價的詳細資訊，請參閱下列資源︰</span><span class="sxs-lookup"><span data-stu-id="502ac-172">For more information about Azure virtual-machine sizes and pricing, see the following resources:</span></span>

* <span data-ttu-id="502ac-173">Azure 虛擬機器大小</span><span class="sxs-lookup"><span data-stu-id="502ac-173">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="502ac-174">[Azure 中的 Windows 虛擬機器大小]</span><span class="sxs-lookup"><span data-stu-id="502ac-174">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="502ac-175">[Azure 中的 Linux 虛擬機器大小]</span><span class="sxs-lookup"><span data-stu-id="502ac-175">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="502ac-176">Azure 虛擬機器定價</span><span class="sxs-lookup"><span data-stu-id="502ac-176">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="502ac-177">[Windows 虛擬機器定價]</span><span class="sxs-lookup"><span data-stu-id="502ac-177">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="502ac-178">[Linux 虛擬機器定價]</span><span class="sxs-lookup"><span data-stu-id="502ac-178">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="502ac-179">如需適用於 Java IDE 的 Azure 套件組的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="502ac-179">For more information about the Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="502ac-180">[適用於 Eclipse 的 Azure 工具組]</span><span class="sxs-lookup"><span data-stu-id="502ac-180">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="502ac-181">[Azure Toolkit for Eclipse 的新功能]</span><span class="sxs-lookup"><span data-stu-id="502ac-181">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="502ac-182">[安裝 Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="502ac-182">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="502ac-183">[Azure Toolkit for Eclipse 的登入指示]</span><span class="sxs-lookup"><span data-stu-id="502ac-183">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="502ac-184">[在 Eclipse 中建立 Azure Hello World Web 應用程式]</span><span class="sxs-lookup"><span data-stu-id="502ac-184">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="502ac-185">[Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="502ac-185">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="502ac-186">[適用於 IntelliJ 的 Azure 工具組新增功能]</span><span class="sxs-lookup"><span data-stu-id="502ac-186">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="502ac-187">[安裝 Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="502ac-187">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="502ac-188">[適用於 IntelliJ 的 Azure 工具組登入指示]</span><span class="sxs-lookup"><span data-stu-id="502ac-188">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="502ac-189">[在 IntelliJ 中建立 Azure Hello World Web 應用程式]</span><span class="sxs-lookup"><span data-stu-id="502ac-189">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="502ac-190">如需有關使用 Azure 搭配 Java 的詳細資訊，請參閱 [Azure Java 開發人員中心]和[適用於 Visual Studio Team Services 的 Java 工具]。</span><span class="sxs-lookup"><span data-stu-id="502ac-190">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="502ac-191">[適用於 Eclipse 的 Azure 工具組]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="502ac-191">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="502ac-192">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="502ac-192">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="502ac-193">[在 Eclipse 中建立 Azure Hello World Web 應用程式]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="502ac-193">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="502ac-194">[在 IntelliJ 中建立 Azure Hello World Web 應用程式]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="502ac-194">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="502ac-195">[安裝 Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="502ac-195">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="502ac-196">[安裝 Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="502ac-196">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="502ac-197">[Azure Toolkit for Eclipse 的登入指示]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="502ac-197">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="502ac-198">[適用於 IntelliJ 的 Azure 工具組登入指示]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="502ac-198">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="502ac-199">[Azure Toolkit for Eclipse 的新功能]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="502ac-199">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="502ac-200">[適用於 IntelliJ 的 Azure 工具組新增功能]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="502ac-200">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="502ac-201">[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="502ac-201">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="502ac-202">[適用於 Visual Studio Team Services 的 Java 工具]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="502ac-202">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="502ac-203">[Azure 中的 Windows 虛擬機器大小]: /azure/virtual-machines/virtual-machines-windows-sizes</span><span class="sxs-lookup"><span data-stu-id="502ac-203">[Sizes for Windows virtual machines in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span></span>
<span data-ttu-id="502ac-204">[Azure 中的 Linux 虛擬機器大小]: /azure/virtual-machines/virtual-machines-linux-sizes</span><span class="sxs-lookup"><span data-stu-id="502ac-204">[Sizes for Linux virtual machines in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span></span>
<span data-ttu-id="502ac-205">[Windows 虛擬機器定價]: /pricing/details/virtual-machines/windows/</span><span class="sxs-lookup"><span data-stu-id="502ac-205">[Windows virtual-machine pricing]: /pricing/details/virtual-machines/windows/</span></span>
<span data-ttu-id="502ac-206">[Linux 虛擬機器定價]: /pricing/details/virtual-machines/linux/</span><span class="sxs-lookup"><span data-stu-id="502ac-206">[Linux virtual-machine pricing]: /pricing/details/virtual-machines/linux/</span></span>


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
