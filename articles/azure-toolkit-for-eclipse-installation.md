---
title: "aaaInstalling hello Azure Toolkit for Eclipse |Microsoft 文件"
description: "了解如何 tooinstall hello Azure Toolkit for Eclipse。"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6c195fab2b47fb5c42541a8cf52be4ec88d27b5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="installing-hello-azure-toolkit-for-eclipse"></a>安裝 Azure Toolkit for Eclipse hello
hello Azure Toolkit for Eclipse 提供範本和功能，可讓您 tooeasily 建立、 開發、 測試和部署 Azure 應用程式使用 hello Eclipse 開發環境。 hello Azure Toolkit for Eclipse 是開放原始碼專案。 hello 原始程式碼時才可使用 hello MIT 授權從<https://github.com/microsoft/azure-tools-for-java>。

hello 下列步驟顯示如何 tooinstall hello Azure Toolkit for Eclipse。

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="tooinstall-hello-azure-toolkit-for-eclipse"></a>tooinstall hello Azure Toolkit for Eclipse
1. 啟動 Eclipse。
2. 按一下 hello**協助**功能表，然後再按一下**安裝新軟體**hello 下列圖例所示。
   
    ![安裝 Azure Toolkit for Eclipse hello][01]
3. 在 hello**可用軟體**hello 對話方塊，**搭配**文字方塊中，輸入`http://dl.microsoft.com/eclipse`後面接著 hello **Enter**索引鍵。
4. 在 [hello**名稱**] 窗格中，核取**Azure Toolkit for Eclipse**，並取消核取**期間聯絡所有更新網站安裝所需的 toofind 軟體**。 您的畫面應該會出現類似 toohello 下列：
   
    ![安裝 Azure Toolkit for Eclipse hello][02]
5. 如果您展開 hello **Azure Toolkit for Eclipse**，您會看到下列項目 hello:
   
   * **Application Insights Plugin for Java**： 此元件可讓您 toouse Azure 的遙測記錄和分析服務應用程式與伺服器執行個體。
   * **Azure 存取控制服務篩選**： 此元件提供驗證應用程式使用者以 Azure ACS、 啟用單一登入案例和支援具體化識別邏輯與 hello 應用程式。
   * **Azure Common Plugin**： 此元件提供 hello 其他工具組元件所需的一般功能。
   * **適用於 Eclipse 的 azure Explorer**： 此元件提供 hello 其他工具組元件所需的一般功能。
   * **Azure Plugin for Eclipse with Java**： 此元件提供支援開發協助建置、 測試及部署 hello Microsoft Azure 雲端在 Eclipse 中，並透過命令列的 Java 應用程式的專案。
   * **使用 Java 的 azure Web 應用程式外掛程式**： 此元件提供支援部署 Java web 應用程式 tooMicrosoft Azure Web 應用程式容器。
   * **Microsoft JDBC Driver 4.2 for SQL Server**：這個元件提供適用於 SQL Server 的 JDBC API 以及適用於 Java Platform Enterprise Edition 8 的 Microsoft Azure SQL Database。
   * **Apache Qpid Client Libraries for JMS 套件**： 此元件提供 hello JMS 用戶端元件 hello Apache Qpid 專案 tooenable 從您的應用程式 toouse AMQP 訊息在 Microsoft Azure 中。
   * **Package for Microsoft Azure Libraries for Java**：此元件提供用來存取 Microsoft Azure 服務 (例如儲存體、服務匯流排、服務執行階段等) 的 API。
6. 按一下 [下一步] 。 (如果安裝 hello 工具組時，您會遇到不尋常的延遲，請確認**期間聯絡所有更新網站安裝軟體所需的 toofind**未核取。)
7. 在 [hello**安裝詳細資料**] 對話方塊中，按一下**下一步**。
   
    ![檢閱安裝詳細資料][03]
8. 在 [hello**檢閱授權**] 對話方塊中，檢閱 hello hello 授權合約條款。 如果您接受 hello hello 授權合約條款，請按一下**我接受 hello hello 授權合約條款**，然後按一下**完成**。 （hello 其餘步驟假設您接受 hello hello 授權合約的條款。 如果您不接受 hello hello 授權合約條款，結束 hello 安裝程序。）
   
    ![檢閱授權][04]
   
    Eclipse 會下載並安裝 hello 必要封裝。
   
    ![安裝進度][05]
9. 如果系統提示 toorestart Eclipse toocomplete 安裝，請按一下**是**。
   
    ![重新啟動提示][06]

## <a name="see-also"></a>另請參閱
針對 Java Ide hello Azure 工具套件的相關資訊，請參閱下列連結查看 hello:

* [適用於 Eclipse 的 Azure 工具組]
  * [功能 hello Azure Toolkit for Eclipse 中的新功能]
  * *安裝 hello Azure Toolkit for Eclipse （此文件）*
  * [符號中的指示 hello Azure Toolkit for Eclipse]
  * [Create a Hello World Web App for Azure in Eclipse (在 Eclipse 中建立 Azure Hello World Web 應用程式)]
* [Azure Toolkit for IntelliJ]
  * [新功能 hello Azure Toolkit for IntelliJ]
  * [安裝 hello Azure Toolkit for IntelliJ]
  * [符號中的 hello Azure Toolkit for IntelliJ 指示]
  * [在 IntelliJ 中建立 Azure Hello World Web 應用程式]

如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心]。

<!-- URL List -->

[適用於 Eclipse 的 Azure 工具組]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md
[Create a Hello World Web App for Azure in Eclipse (在 Eclipse 中建立 Azure Hello World Web 應用程式)]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[在 IntelliJ 中建立 Azure Hello World Web 應用程式]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Installing hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[安裝 hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[符號中的指示 hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[符號中的 hello Azure Toolkit for IntelliJ 指示]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[功能 hello Azure Toolkit for Eclipse 中的新功能]: ./azure-toolkit-for-eclipse-whats-new.md
[新功能 hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->
