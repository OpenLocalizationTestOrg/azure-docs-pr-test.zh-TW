---
title: "aaaSign 中的指示 hello Azure Toolkit for IntelliJ |Microsoft 文件"
description: "了解如何 toosign 中使用 tooMicrosoft Azure hello Azure Toolkit IntelliJ。"
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
ms.openlocfilehash: 2de781fc19267cce133b1e6456481497e165fce4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-instructions-for-hello-azure-toolkit-for-intellij"></a>登入的指示 hello Azure Toolkit for IntelliJ

hello Azure Toolkit for IntelliJ 提供兩種方法在 tooyour Azure 帳戶登入：

  * **互動式**： 您在 tooyour Azure 帳戶中輸入您的 Azure 認證每次您登入。
  * **自動化**： 您建立的認證檔案，您可以使用 tooautomatically 登 tooyour Azure 帳戶中。

hello 下列各節說明如何 toouse 每一種方法。

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-tooyour-azure-account-interactively"></a>以互動方式登入 tooyour Azure 帳戶

在手動輸入您的 Azure 認證 tooAzure toosign hello 遵循：

1. 使用 IntelliJ IDEA 開啟您的專案。

2. 按一下**工具**，點太**Azure**，然後按一下 **Azure 登入**。

   ![hello IntelliJ Azure 登入 命令][I01]

3. 在 hello **Azure 登入**視窗中，選取**互動式**，然後按一下**登入**。

   ![hello Azure 登入與選取的 Interactive 視窗][I02]

4. 在 hello **Azure 登入**出現對話方塊，請輸入您的 Azure 認證，然後按一下**登入**。

   ![hello Azure 登入 對話方塊視窗][I03]

5. 在 hello**選取的訂用帳戶**對話方塊中，選取 hello 訂閱您想 toouse，然後再按一下**確定**。

   ![hello 選取多個訂閱對話方塊][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a>在以互動方式登入後，登出您的 Azure 帳戶

您已使用 hello 先前步驟來設定您的帳戶之後，您將會自動登出您的 Azure 帳戶，每次您重新啟動 IntelliJ 概念。 不過，如果想要從您的 Azure 帳戶的 toosign*沒有*IntelliJ 概念，重新啟動之後執行 hello。

1. 在 IntelliJ 概念，在 hello**工具**功能表上，點太**Azure**，然後按一下 **Azure 登出**。

   ![hello IntelliJ Azure 登出命令][L01]

2. 在 hello **Azure 登出**確認視窗中，按一下 **是**。

   ![hello Azure 登出確認視窗][L02]

## <a name="sign-in-tooyour-azure-account-automatically"></a>自動登入 tooyour Azure 帳戶

本節會逐步引導您建立認證檔案，並在檔案中包含您的服務主體資料。 您已完成此程序之後，Eclipse 使用 hello 認證檔案 tooautomatically 登中 tooAzure 每次開啟專案。

1. 使用 IntelliJ IDEA 開啟您的專案。

2. 在 hello**工具**功能表上，點太**Azure**，然後按一下 **Azure 登入**。

   ![hello IntelliJ Azure 登入 命令][A01]

3. 在 hello **Azure 登入**視窗中，選取**自動化**，然後按一下**新增**。

   ![hello Azure 登入與自動選取視窗][A02]

4. 在 hello **Azure 登入對話方塊**視窗中，輸入您的 Azure 認證，然後按一下**登入**。

   ![hello Azure 登入 對話方塊視窗][A03]

5. 在 hello**建立驗證檔案**視窗中，選取 hello 訂閱您想 toouse，選擇您的目的地目錄，然後按一下**啟動**。

   ![hello 驗證檔建立視窗][A04]

6. 在 hello**服務主體建立狀態**對話方塊中，已成功建立您的檔案之後，請按一下**確定**。

   ![hello 服務主體建立狀態 對話方塊][A05]

7. 在 hello **Azure 登入**視窗中，按一下 **登入**。

   ![[Azure 登入] 對話方塊][A06]

8. 在 hello**選取的訂用帳戶**對話方塊中，選取 hello 訂閱您想 toouse，然後再按一下**確定**。

   ![hello 選取多個訂閱對話方塊][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a>在自動登入後登出您的 Azure 帳戶

您已使用 hello 先前步驟來設定您的帳戶之後，hello Azure Toolkit 會自動將您登入 tooyour 每次您重新啟動 IntelliJ 概念的 Azure 帳戶。 不過，toosign 您的 Azure 帳戶的資料，並防止 hello Azure Toolkit 從您自動登入，請勿 hello 遵循：

1. 在 IntelliJ 概念，在 hello**工具**功能表上，點太**Azure**，然後按一下 **Azure 登出**。

   ![hello IntelliJ Azure 登出命令][L01]

2. 在 hello **Azure 登出**確認視窗中，按一下 **是**。

   ![hello Azure 登出確認視窗][L03]

## <a name="sign-in-tooyour-azure-account-automatically-by-using-an-existing-credentials-file"></a>自動登入 tooyour Azure 帳戶使用現有的認證檔案

如果您會登出您的 Azure 帳戶，當您使用 IntelliJ 概念時，您必須使用現有的認證檔案 tooautomatically 登入 toohello 帳戶。 tooconfigure hello Azure Toolkit for Eclipse toouse 現有的認證檔案，請勿 hello 遵循：

1. 使用 IntelliJ IDEA 開啟您的專案。

2. 在 hello**工具**功能表上，點太**Azure**，然後按一下 **Azure 登入**。

   ![hello IntelliJ Azure 登入 命令][A01]

3. 在 hello **Azure 登入**視窗中，選取**自動化**，然後按一下**瀏覽**。

   ![hello Azure 登入與自動選取視窗][A02]

4. 在 hello**選取驗證檔案**對話方塊中，選取先前建立的認證檔案，然後按一下**選取**。

   ![hello 選取驗證檔案對話方塊][A08]

5. 在 hello **Azure 登入**視窗中，按一下 **登入**。

   ![hello Azure 登入與自動選取視窗][A06]

6. 在 hello**選取的訂用帳戶**對話方塊中，選取 hello 訂閱您想 toouse，然後再按一下**確定**。

   ![hello 選取多個訂閱對話方塊][A07]

## <a name="next-steps"></a>後續步驟
針對 Java Ide hello Azure 工具套件的相關資訊，請參閱下列連結查看 hello:

* [適用於 Eclipse 的 Azure 工具組]
  * [在 hello Azure Toolkit for Eclipse 中最新消息]
  * [安裝 Azure Toolkit for Eclipse hello]
  * [登入指示 hello Azure Toolkit for Eclipse]
  * [在 Eclipse 中建立 Azure Hello World Web 應用程式]
* [Azure Toolkit for IntelliJ]
  * [在 hello Azure Toolkit for IntelliJ 最新消息]
  * [安裝 hello Azure Toolkit for IntelliJ]
  * *登入的指示 hello Azure Toolkit for IntelliJ* （即本文）
  * [在 IntelliJ 中建立 Azure Hello World Web 應用程式]

如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心]和 hello [Java 工具的 Visual Studio Team Services]。

<!-- URL List -->

[適用於 Eclipse 的 Azure 工具組]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md
[在 Eclipse 中建立 Azure Hello World Web 應用程式]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[在 IntelliJ 中建立 Azure Hello World Web 應用程式]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[安裝 Azure Toolkit for Eclipse hello]: ./azure-toolkit-for-eclipse-installation.md
[安裝 hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[登入指示 hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Sign-in instructions for hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[在 hello Azure Toolkit for Eclipse 中最新消息]: ./azure-toolkit-for-eclipse-whats-new.md
[在 hello Azure Toolkit for IntelliJ 最新消息]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/
[Java 工具的 Visual Studio Team Services]: https://java.visualstudio.com/

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L03.png
