---
title: "aaaMake 虛擬機器可用的 tooyour Azure 堆疊使用者 |Microsoft 文件"
description: "提供 Azure 堆疊上的教學課程 toomake 虛擬機器"
services: azure-stack
documentationcenter: 
author: vhorne
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/22/2017
ms.author: victorh
ms.custom: mvc
ms.openlocfilehash: 345206912f17662e51341c71175c5fe87b692ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="make-virtual-machines-available-tooyour-azure-stack-users"></a>讓虛擬機器可用 tooyour Azure 堆疊使用者
Azure 堆疊的雲端系統管理員，您可以建立您的使用者 （有時參照的 tooas 租用戶） 可以訂閱的優惠。 利用其訂用帳戶，使用者可以接著取用 Azure Stack 服務。

本文章將示範如何 toocreate 的供應項目，然後進行測試。 Hello 測試中，您將登入 toohello 入口網站的使用者身分，訂閱 toohello 供應項目，然後再建立虛擬機器使用 hello 訂用帳戶。

您將了解：

> [!div class="checklist"]
> * 建立優惠
> * 新增映像
> * 測試 hello 優惠


Azure 堆疊中的服務會傳遞 toousers 使用訂用帳戶、 提供項目，以及計劃。 使用者可以訂閱 toomultiple 優惠。 優惠可以有一個或多個方案，而方案則可有一或多項服務。

![訂用帳戶、供應項目與方案](media/azure-stack-key-features/image4.png)

詳細資訊，請參閱 toolearn[主要功能和 Azure 堆疊中的概念](azure-stack-key-features.md)。

## <a name="create-an-offer"></a>建立優惠

現在您可以為使用者準備項目。 當您啟動 hello 程序時，您是第一個提示的 toocreate hello 優惠，計劃，然後按一下最後配額。

3. **建立優惠**

   提供項目是一或多個計劃的群組有 toousers toopurchase 該提供者或訂閱。

   a. [登入](azure-stack-connect-azure-stack.md)toohello 網站中的做為雲端系統管理員，然後按一下**新增** > **租用戶提供 + 計劃** > **提供**。
   ![新增供應項目](media/azure-stack-tutorial-tenant-vm/image01.png)

   b. 在 hello**新提供**區段中，填寫**顯示名稱**和**資源名稱**，，然後選取新的或現有**資源群組**。 hello 顯示名稱會是 hello 供應項目的易記名稱。 Hello 雲端操作員可以看到 hello 資源名稱。 它的 hello 名稱，系統管理員 」 搭配 toowork hello 供應項目做為 Azure 資源管理員資源。

   ![顯示名稱](media/azure-stack-tutorial-tenant-vm/image02.png)

   c. 按一下**基底計劃**，並在 hello**計劃**區段中，按一下**新增**tooadd 新的計劃 toohello 優惠。

   ![新增方案](media/azure-stack-tutorial-tenant-vm/image03.png)

   d. 在 hello**新增計劃**區段中，填寫**顯示名稱**和**資源名稱**。 hello 顯示名稱是使用者看到的 hello 計劃的易記名稱。 Hello 雲端操作員可以看到 hello 資源名稱。 它的 hello 名稱，雲端操作員搭配 toowork hello 計劃做為 Azure 資源管理員資源。

   ![方案顯示名稱](media/azure-stack-tutorial-tenant-vm/image04.png)

   e. 按一下 服務，選取 Microsoft.Compute、Microsoft.Network 及 Microsoft.Storage，然後按一下選取。

   ![方案服務](media/azure-stack-tutorial-tenant-vm/image05.png)

   f. 按一下**配額**，然後選取您想要的 toocreate 配額 hello 第一個服務。 IaaS 配額，請遵循下列步驟 hello 運算、 網路和儲存體服務。

   在此範例中，我們會先建立 hello 計算服務的配額。 在 hello 命名空間清單中，選取 hello **Microsoft.Compute**命名空間，然後按一下**建立新的配額**。
   
   ![建立新的配額](media/azure-stack-tutorial-tenant-vm/image06.png)

   g. 在 hello**建立配額**區段中，輸入 hello 配額以及組 hello hello 配額，然後按一下所需的參數名稱**確定**。

   ![配額名稱](media/azure-stack-tutorial-tenant-vm/image07.png)

   h. 現在，如**Microsoft.Compute**，選取您建立的 hello 配額。

   ![選取配額](media/azure-stack-tutorial-tenant-vm/image08.png)

   重複這些步驟 hello 網路和儲存體服務，然後再按一下**確定**上 hello**配額**> 一節。

   i. 按一下**確定**上 hello**新計劃**> 一節。

   j. 在 hello**計劃**區段中選取 hello 新計劃，然後按一下**選取**。

   k. 在 hello**新的優惠**區段中，按一下**建立**。 在建立 hello 優惠時，您會看到通知。

   l. Hello 儀表板功能表上，按一下**提供**然後按一下您所建立的 hello 供應項目。

   m. 按一下 變更狀態，然後按一下公開。

   ![公開映像](media/azure-stack-tutorial-tenant-vm/image09.png)

## <a name="add-an-image"></a>新增映像

您可以佈建虛擬機器之前，您必須加入的映像 toohello 堆疊 Azure marketplace。 您可以加入您的選擇，包括 Linux 映像，從 hello Azure Marketplace 的 hello 映像。

如果您正在連線的案例中，而且如果您註冊 Azure 與您 Azure 堆疊的執行個體，然後您可以下載 hello Windows Server 2016 VM 映像從 hello Azure Marketplace 使用 hello hello 中所述的步驟[下載marketplace 項目，從 Azure tooAzure 堆疊](azure-stack-download-azure-marketplace-item.md)主題。

如需新增不同的項目 toohello marketplace 資訊，請參閱[hello Marketplace</堆疊](azure-stack-marketplace.md)。

## <a name="test-hello-offer"></a>測試 hello 優惠

既然您已經建立供應項目，您可以進行測試。 以使用者身分登入和訂閱 toohello 供應項目，然後將虛擬機器。

1. **訂閱 tooan 供應項目**

   現在您可以登入 toohello 入口網站為使用者 toosubscribe tooan 供應項目。

   a. Hello Azure 堆疊部署套件在電腦上，登入太`https://portal.local.azurestack.external`作為使用者按一下**取得訂用帳戶**。

   ![取得訂用帳戶](media/azure-stack-subscribe-plan-provision-vm/image01.png)

   b. 在 hello**顯示名稱**欄位中，輸入您的訂用帳戶的名稱，按一下**提供**，按一下其中一個 hello hello 優惠**選擇優惠**區段，，然後按一下 **建立**。

   ![建立優惠](media/azure-stack-subscribe-plan-provision-vm/image02.png)

   c. 建立 tooview hello 訂用帳戶中，按一下**更多服務**，按一下 **訂閱**，然後按一下 新的訂用。  

   訂閱 tooan 供應項目之後，重新整理 hello 入口 toosee 哪些服務為 hello 新訂閱的一部分。

2. **佈建虛擬機器**

   現在您可以登入 toohello 入口網站為使用者 tooprovision 使用 hello 訂用帳戶在虛擬機器。 

   a. Hello Azure 堆疊部署套件在電腦上，登入太`https://portal.local.azurestack.external`作為使用者，然後按一下**新增** > **計算** > **Windows Server 2016 DatacenterEval**。  

   b. 在 hello**基本概念**區段中，輸入**名稱**，**使用者名**，和**密碼**。 針對 [VM 磁碟類型]，請選擇 [HDD]。 選擇 [訂用帳戶] 。 建立 資源群組，或選取現有的資源群組，然後按一下確定。  

   c. 在 hello**大小選擇 「**區段中，按一下**A1 基本**，然後按一下**選取**。  

   d. 在 hello**設定**區段中，按一下**虛擬網路**。 在 hello**選擇虛擬網路**區段中，按一下**建立新**。 在 hello**建立虛擬網路**區段中，接受所有的 hello 預設值，然後按一下 **確定**。 在 hello**設定**區段中，按一下**確定**。

   ![建立虛擬網路](media/azure-stack-provision-vm/image04.png)

   e. 在 hello**摘要**區段中，按一下**確定**toocreate hello 虛擬機器。  

   f. toosee 新的虛擬機器，按一下 **所有資源**，然後搜尋 hello 虛擬機器，然後按一下其名稱。

    ![所有資源](media/azure-stack-provision-vm/image06.png)

在本教學課程中，您已了解：

> [!div class="checklist"]
> * 建立優惠
> * 新增映像
> * 測試 hello 優惠

> [!div class="nextstepaction"]
> [讓 web、 行動裝置、 應用程式開發介面應用程式可用 tooyour Azure 堆疊使用者](azure-stack-tutorial-app-service.md)
