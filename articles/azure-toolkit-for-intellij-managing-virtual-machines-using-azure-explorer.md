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
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-intellij"></a>管理虛擬機器使用 IntelliJ hello Azure 總管

hello Azure 總管 中，這是 hello Azure Toolkit for IntelliJ 的一部分，提供 Java 開發人員容易使用的解決方案來管理從其 Azure 帳戶中的虛擬機器 hello IntelliJ 整合式的開發環境 (IDE) 內。

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a>在 IntelliJ 中建立虛擬機器

請勿 hello toocreate 使用 hello Azure 總管 中，虛擬機器，遵循： 

1. 登入 tooyour Azure 帳戶，使用中 hello hello 步驟[登入的指示 hello Azure Toolkit for IntelliJ]發行項。

2. 在 hello **Azure 總管**檢視中，展開 hello **Azure**  節點，以滑鼠右鍵按一下**虛擬機器**，然後按一下**建立 VM**。 

   ![hello 建立 VM 命令][CR01]  
    hello**建立新的虛擬機器**精靈 隨即開啟。

3. 在 hello**選擇訂用帳戶**視窗中，選取您的訂閱，然後按一下**下一步**。 

   ![hello 選擇訂用帳戶視窗][CR02]

4. 在 hello**選取虛擬機器映像**視窗中，輸入下列資訊的 hello:

   * **位置**︰指定要建立虛擬機器的位置 (例如「美國西部」)。 

   * **建議的映像**︰指定您會從常用映像的簡短清單中選擇映像。

   * **自訂映像**： 指定您會藉由提供下列資訊的 hello 選擇自訂映像：

      * **發行者**： 指定建立 hello 映像，您將使用您的虛擬機器的 hello 發行者 (例如， *Microsoft*)。

      * **提供**： 指定從 hello 選取 「 發行者 」 提供 toouse hello 虛擬機器 (例如， *JDK*)。

      * **Sku**： 指定 hello stockkeeping 單位 (SKU) toouse 從 hello 選供應項目 (例如， *JDK_8*)。

      * **版本 #**： 指定哪個版本的 hello 選取 SKU toouse。

   ![選擇虛擬機器映像期間 hello][CR03]

5. 按一下 [下一步] 。 

6. 在 hello**虛擬機器基本設定**視窗中，輸入下列資訊的 hello:

   * **虛擬機器名稱**： 指定新的虛擬機器，必須以字母開頭且只能包含字母、 數字和連字號 hello 名稱。

   * **大小**： 指定 hello 的核心數目和您的虛擬機器的記憶體 tooallocate。

   * **使用者名稱**： 指定 hello 系統管理員帳戶 toocreate 來管理您的虛擬機器。

   * **密碼**和**確認**： 指定 hello 系統管理員帳戶的密碼。

   ![hello 虛擬機器基本設定 視窗][CR04]

7. 按一下 [下一步] 。 

8. 在 hello**相關聯的資源**視窗中，輸入下列資訊的 hello:

   * **資源群組**： 指定您的虛擬機器的 hello 資源群組。 選取其中一個 hello 下列選項：
      * **建立新**： 指定您想 toocreate 新的資源群組。
      * **使用現有**： 指定您想 tooselect 從您的 Azure 帳戶相關聯的資源群組的清單。

       ![hello 相關聯資源的視窗][CR07]

   * **儲存體帳戶**： 指定 hello 儲存體帳戶 toouse 來儲存您的虛擬機器。 您可以選擇現有儲存體帳戶或建立新的帳戶。 如果您選擇**新建**，會出現下列對話方塊中的 hello:

      ![hello 建立儲存體帳戶對話方塊][CR05]

   * **虛擬網路**和**子網路**： 指定 hello 虛擬網路與虛擬機器會連接到的子網路。 您可以使用現有的網路和子網路，也可以建立新的網路和子網路。 如果您選取**建立新**，會出現下列對話方塊中的 hello:

      ![hello 建立虛擬網路 對話方塊][CR06]

   * **公用 IP 位址**︰指定虛擬機器的對外 IP 位址。 您可以選擇 toocreate 新的 IP 位址，或者如果您的虛擬機器不會有公用 IP 位址，您可以選取**（無）**。 

   * **網路安全性群組**︰為虛擬機器指定選用的網路防火牆。 您可以選取現有防火牆，但如果虛擬機器不會使用網路防火牆，您也可以選取 [(無)]。 

   * **可用性設定組**︰指定虛擬機器可以加入的選用可用性設定組。 您可以選取現有的可用性設定組，建立新的可用性設定組或，如果您的虛擬機器將不屬於 tooan 可用性設定組中，選取**（無）**。

9. 按一下 [完成] 。  
    新的虛擬機器會出現在 hello Azure 總管工具視窗。 

   ![Hello Azure 總管檢視中的新虛擬機器][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a>在 IntelliJ 中重新啟動虛擬機器

請勿 hello toorestart 利用 hello Azure 總管 IntelliJ，虛擬機器，遵循：

1. 在 hello **Azure 總管**檢視、 hello 虛擬機器，以滑鼠右鍵按一下，然後選取**重新啟動**。

   ![hello 虛擬機器重新啟動命令][RE01]

2. 在 hello 確認視窗中，按一下 **是**。 

   ![hello 重新啟動虛擬機器確認視窗][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a>在 IntelliJ 中將虛擬機器關機

關閉執行中虛擬機器中 IntelliJ，使用 hello Azure 總管 tooshut hello 遵循：

1. 在 hello **Azure 總管**檢視、 hello 虛擬機器，以滑鼠右鍵按一下，然後選取**關機**。

   ![hello 虛擬機器關機命令][SH01]

2. 在 hello 確認視窗中，按一下 **是**。 

   ![關閉虛擬機器確認視窗中的 hello][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a>在 IntelliJ 中刪除虛擬機器

請勿 hello toodelete 利用 hello Azure 總管 IntelliJ，虛擬機器，遵循：

1. 在 hello **Azure 總管**檢視、 hello 虛擬機器，以滑鼠右鍵按一下，然後選取**刪除**。

   ![hello 虛擬機器的 Delete 命令][DE01]

2. 在 hello 確認視窗中，按一下 **是**。 

   ![hello 刪除虛擬機器確認視窗][DE02]

## <a name="next-steps"></a>後續步驟
如需 Azure 的虛擬機器大小和定價的詳細資訊，請參閱下列資源的 hello:

* Azure 虛擬機器大小
  * [Azure 中的 Windows 虛擬機器大小]
  * [Azure 中的 Linux 虛擬機器大小]
* Azure 虛擬機器定價
  * [Windows 虛擬機器定價]
  * [Linux 虛擬機器定價]

針對 Java Ide hello Azure 工具套件的相關資訊，請參閱下列資源的 hello:

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
