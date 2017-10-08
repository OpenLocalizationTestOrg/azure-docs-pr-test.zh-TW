---
title: "aaaSign 中指示的 hello Azure Toolkit for Eclipse |Microsoft 文件"
description: "了解如何使用 Microsoft Azure 到 toosign hello Azure Toolkit for Eclipse。"
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
ms.openlocfilehash: 95be64750ca0147f76dae8f364fad80cb9ccc969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sign-in-instructions-for-hello-azure-toolkit-for-eclipse"></a>Azure 登中的指示 hello Azure Toolkit for Eclipse

hello Azure Toolkit for Eclipse 提供兩種方法來登入您的 Azure 帳戶：

  * **互動式** - 當您使用這個方法時，每次登入 Azure 帳戶都要輸入 Azure 認證。
  * **自動化**-當您使用此方法中，您將建立包含您服務主體的資料之後, 您可以使用 hello 認證檔案 tooautomatically 登入您的 Azure 帳戶的認證檔案。

hello hello 下列各節中的步驟將說明如何 toouse 每一種方法。

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a>以互動方式登入您的 Azure 帳戶

hello 下列步驟將說明如何以手動輸入您的 Azure 認證的 toosign 至 Azure。

1. 使用 Eclipse 開啟您的專案。

1. 依序按一下 [工具]、[Azure] 以及 [登入]。

   ![Azure 登入的 Eclipse 功能表][I01]

1. 當 hello **Azure 登入**對話方塊出現，請選取**互動式**，然後按一下**登入**。

   ![[登入] 對話方塊][I02]

1. 當 hello **Azure 登入**出現對話方塊，請輸入您的 Azure 認證，然後按一下**登入**。

   ![[Azure 登入] 對話方塊][I03]

1. 當 hello**選取的訂用帳戶**出現對話方塊，請選取 hello 訂閱您想 toouse，然後再按一下**確定**。

   ![[選取訂用帳戶] 對話方塊][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a>當您以互動方式登入時，登出您的 Azure 帳戶

Hello 前一節中設定 hello 步驟之後，您將會自動登出您每次您重新啟動 Eclipse 的 Azure 帳戶。 不過，如果您想 toosign 超出您的 Azure 帳戶不需要重新啟動 Eclipse，使用下列步驟的 hello。

1. 在 Eclipse 中，依序按一下 [工具]、[Azure] 以及 [登出]。

   ![Azure 登出的 Eclipse 功能表][L01]

1. 當 hello **Azure 登出**對話方塊出現時，按一下**是**。

   ![[登出] 對話方塊][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-toouse-in-hello-future"></a>自動登入您的 Azure 帳戶，建立的認證檔案 toouse hello 未來

hello 下列步驟將引導您完成建立包含您的服務主體資料的認證檔案。 當您完成這些步驟，Eclipse 便會自動使用 hello 認證檔案 tooautomatically 登您到 Azure，每次您開啟您的專案。

1. 使用 Eclipse 開啟您的專案。

1. 依序按一下 [工具]、[Azure] 以及 [登入]。

   ![Azure 登入的 Eclipse 功能表][A01]

1. 當 hello **Azure 登入**對話方塊出現，請選取**自動化**，然後按一下**新增**。

   ![[登入] 對話方塊][A02]

1. 當 hello **Azure 登入**出現對話方塊，請輸入您的 Azure 認證，然後按一下**登入**。

   ![[Azure 登入] 對話方塊][A03]

1. 當 hello**建立驗證檔案**出現對話方塊，請選取 hello 訂閱您想 toouse，選擇您的目的地目錄，然後按一下**啟動**。

   ![[Azure 登入] 對話方塊][A04]

1. hello**服務主體 Creatation 狀態**會顯示對話方塊，並且已成功建立您的檔案之後，按一下 **確定**。

   ![[服務主體建立狀態] 對話方塊][A05]

1. 當 hello **Azure 登入**對話方塊出現時，按一下**登入**。

   ![[Azure 登入] 對話方塊][A06]

1. 當 hello**選取的訂用帳戶**出現對話方塊，請選取 hello 訂閱您想 toouse，然後再按一下**確定**。

   ![[選取訂用帳戶] 對話方塊][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a>當您以自動化方式登入時，登出您的 Azure 帳戶

Hello 前一節中設定 hello 步驟之後，hello Azure Toolkit 可自動登入您每次您重新啟動 Eclipse 的 Azure 帳戶。 不過，toosign 超出您的 Azure 帳戶，以及防止 hello Azure Toolkit 您登入自動，會使用下列步驟的 hello。

1. 在 Eclipse 中，依序按一下 [工具]、[Azure] 以及 [登出]。

   ![Azure 登出的 Eclipse 功能表][L01]

1. 當 hello **Azure 登出**對話方塊出現時，按一下**是**。

   ![[登出] 對話方塊][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a>使用已建立的認證檔案來自動登入 Azure 帳戶

如果您會登出 Azure，當您使用 Eclipse，您必須 tooreconfigure hello Azure Toolkit for Eclipse toouse 建立之前，您可以自動登入您的 Azure 帳戶的認證檔案。 hello 下列步驟將引導您完成設定 hello Azure Toolkit toouse 現有的憑證檔案。

1. 使用 Eclipse 開啟您的專案。

1. 依序按一下 [工具]、[Azure] 以及 [登入]。

   ![Azure 登入的 Eclipse 功能表][A01]

1. 當 hello **Azure 登入**對話方塊出現，請選取**自動化**，然後按一下**瀏覽**。

   ![[登入] 對話方塊][A02]

1. 當 hello**選取驗證檔案**出現對話方塊，請選取您稍早建立的認證檔案，然後按一下**選取**。

   ![[登入] 對話方塊][A08]

1. 當 hello **Azure 登入**對話方塊出現時，按一下**登入**。

   ![[Azure 登入] 對話方塊][A06]

1. 當 hello**選取的訂用帳戶**出現對話方塊，請選取 hello 訂閱您想 toouse，然後再按一下**確定**。

   ![[選取訂用帳戶] 對話方塊][A07]

## <a name="see-also"></a>另請參閱
針對 Java Ide hello Azure 工具套件的相關資訊，請參閱下列連結查看 hello:

* [適用於 Eclipse 的 Azure 工具組]
  * [功能 hello Azure Toolkit for Eclipse 中的新功能]
  * [安裝 Azure Toolkit for Eclipse hello]
  * *符號在 hello Azure Toolkit for Eclipse （此文件） 的指示*
  * [Create a Hello World Web App for Azure in Eclipse (在 Eclipse 中建立 Azure Hello World Web 應用程式)]
* [Azure Toolkit for IntelliJ]
  * [新功能 hello Azure Toolkit for IntelliJ]
  * [安裝 hello Azure Toolkit for IntelliJ]
  * [符號中的 hello Azure Toolkit for IntelliJ 指示]
  * [在 IntelliJ 中建立 Azure Hello World Web 應用程式]

如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心]和 hello [Java 工具的 Visual Studio Team Services]。

<!-- URL List -->

[適用於 Eclipse 的 Azure 工具組]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md
[Create a Hello World Web App for Azure in Eclipse (在 Eclipse 中建立 Azure Hello World Web 應用程式)]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[在 IntelliJ 中建立 Azure Hello World Web 應用程式]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[安裝 Azure Toolkit for Eclipse hello]: ./azure-toolkit-for-eclipse-installation.md
[安裝 hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Sign In Instructions for hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[符號中的 hello Azure Toolkit for IntelliJ 指示]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[功能 hello Azure Toolkit for Eclipse 中的新功能]: ./azure-toolkit-for-eclipse-whats-new.md
[新功能 hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/
[Java 工具的 Visual Studio Team Services]: https://java.visualstudio.com/

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L03.png
