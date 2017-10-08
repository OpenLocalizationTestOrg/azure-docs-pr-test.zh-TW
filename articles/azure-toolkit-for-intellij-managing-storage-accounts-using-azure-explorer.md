---
title: "aaaManage 儲存體帳戶使用 IntelliJ hello Azure 總管 |Microsoft 文件"
description: "了解如何 toomanage 您 Azure 儲存體帳戶使用 IntelliJ hello Azure 總管。"
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
ms.openlocfilehash: b094bdcd2fa2782cb12b67c96ac406fbe4c1aa3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-storage-accounts-by-using-hello-azure-explorer-for-intellij"></a>使用 IntelliJ hello Azure 總管來管理儲存體帳戶

hello Azure 總管 中，這是 hello Azure Toolkit for IntelliJ 的一部分，Java 開發人員提供方便使用方案管理從其 Azure 帳戶中的儲存體帳戶內 hello IntelliJ 整合式的開發環境 (IDE)。

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-intellij"></a>在 IntelliJ 中建立儲存體帳戶

toocreate 儲存體帳戶使用 hello Azure 總管 中，請勿 hello 遵循：

1. 使用 hello 登入 Azure 帳戶 tooyour[登入指示 hello Azure Toolkit for Eclipse]。 

2. 在 hello **Azure 總管**檢視中，展開 hello **Azure**  節點，以滑鼠右鍵按一下**儲存體帳戶**，然後按一下**建立儲存體帳戶**.

   ![[建立儲存體帳戶] 命令][CS01]

3. 在 hello**建立儲存體帳戶**對話方塊方塊中，指定下列選項的 hello:

   ![[新建儲存體帳戶] 對話方塊][CS02]

   * **名稱**： 指定 hello hello 新儲存體帳戶名稱。

   * **帳戶類型**： 指定 hello 類型的儲存體帳戶 toocreate （例如，"Blob 儲存 」）。 如需詳細資訊，請參閱[關於 Azure 儲存體帳戶]。 

   * **效能**： 指定提供 toouse 從 hello （例如，「 進階版 」） 的 選取 「 發行者 」 的儲存體帳戶。 如需詳細資訊，請參閱 [Azure 儲存體延展性和效能目標]。 

   * **複寫**： 指定 hello 複寫 hello 儲存體帳戶 （例如，「 區域備援 」）。 如需詳細資訊，請參閱 [Azure 儲存體複寫]。 

   * **訂用帳戶**： 指定 hello toouse 需 hello 新儲存體帳戶的 Azure 訂用帳戶。

   * **位置**： 指定儲存體帳戶 （例如，「 美國西部 」） 的建立位置的 hello 位置。

   * **資源群組**： 指定您的虛擬機器的 hello 資源群組。 選取其中一個 hello 下列選項：
      * **建立新**： 指定您想 toocreate 新的資源群組。
      * **使用現有項目**︰指定您會從 Azure 帳戶相關聯的資源群組清單中進行選擇。

4. 當您指定了所有 hello 上述選項時，按一下 **確定**。

## <a name="create-a-storage-container-in-intellij"></a>在 IntelliJ 中建立儲存體容器

toocreate 使用 hello Azure 總管 中，儲存體容器 hello 遵循：

1. 在 hello Azure 總管檢視，以滑鼠右鍵按一下您想 toocreate 容器，然後再按一下 hello 儲存體帳戶**建立 blob 容器**。

   ![[建立 Blob 容器] 命令][CC01]

2. 在 hello**建立 blob 容器**對話方塊中，指定您的容器，hello 名稱，然後按一下**確定**。 如需為儲存體容器命名的詳細資訊，請參閱[命名和參考容器、Blob 及中繼資料]。

   ![[建立儲存體容器] 對話方塊][CC02]

## <a name="delete-a-storage-container-in-intellij"></a>在 IntelliJ 中刪除儲存體容器

toodelete 使用 hello Azure 總管 中，儲存體容器 hello 遵循：

1. 在 hello Azure 總管檢視，hello 儲存體容器，以滑鼠右鍵按一下，然後按一下**刪除**。

   ![[刪除儲存體容器] 命令][DC01]

2. 在 hello 確認視窗中，按一下 **是**。

   ![刪除儲存體容器的確認視窗][DC02]

## <a name="delete-a-storage-account-in-intellij"></a>在 IntelliJ 中刪除儲存體帳戶

toodelete 儲存體帳戶使用 hello Azure 總管 中，請勿 hello 遵循：

1. 在 hello **Azure 總管**檢視、 hello 儲存體帳戶，以滑鼠右鍵按一下，然後選取**刪除**。

   ![[刪除] 儲存體帳戶功能表][DS01]

2. 在 hello 確認視窗中，按一下 **是**。

   ![刪除儲存體帳戶的確認視窗][DS02]

## <a name="next-steps"></a>後續步驟
如需 Azure 儲存體帳戶、 大小以及價格的詳細資訊，請參閱下列資源的 hello:

* [簡介 tooMicrosoft Azure 儲存體]
* [關於 Azure 儲存體帳戶]
* Azure 儲存體帳戶大小
  * [Azure 中的 Windows 儲存體帳戶大小]
  * [Azure 中的 Linux 儲存體帳戶大小]
* Azure 儲存體帳戶定價
  * [Windows 儲存體帳戶定價]
  * [Linux 儲存體帳戶定價]

Java Ide 的 Azure 工具套件的相關資訊，請參閱下列資源的 hello:

* [適用於 Eclipse 的 Azure 工具組]
  * [在 hello Azure Toolkit for Eclipse 中最新消息]
  * [安裝 Azure Toolkit for Eclipse hello]
  * [登入指示 hello Azure Toolkit for Eclipse]
  * [在 Eclipse 中建立 Azure Hello World Web 應用程式]
* [Azure Toolkit for IntelliJ]
  * [在 hello Azure Toolkit for IntelliJ 最新消息]
  * [安裝 hello Azure Toolkit for IntelliJ]
  * [登入的指示 hello Azure Toolkit for IntelliJ]
  * [在 IntelliJ 中建立 Azure Hello World Web 應用程式]

如需有關使用 Azure 搭配 Java 的詳細資訊，請參閱 [Azure Java 開發人員中心]和[適用於 Visual Studio Team Services 的 Java 工具]。

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

[CS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC02.png
