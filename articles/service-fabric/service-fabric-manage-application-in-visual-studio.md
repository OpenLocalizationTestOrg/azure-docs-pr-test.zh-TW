---
title: "aaaManage Visual Studio 中的應用程式 |Microsoft 文件"
description: "使用 Visual Studio toocreate、 開發，封裝、 部署和偵錯您的 Service Fabric 應用程式和服務。"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: c317cb7e-7eae-466e-ba41-6aa2518be5cf
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: b2d5803d85e4f9645dcbece33a2208bc0955498d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-toosimplify-writing-and-managing-your-service-fabric-applications"></a>使用 Visual Studio toosimplify 撰寫和管理您的 Service Fabric 應用程式
您可以透過 Visual Studio 管理 Azure Service Fabric 應用程式與服務。 一旦您[設定開發環境](service-fabric-get-started.md)，您可以使用 Visual Studio toocreate Service Fabric 應用程式、 加入服務或封裝時，暫存器，並在本機開發叢集部署的應用程式。

## <a name="deploy-your-service-fabric-application"></a>部署 Service Fabric 應用程式
根據預設，部署應用程式結合了下列插入一個簡單的作業步驟的 hello:

1. 建立 hello 應用程式封裝
2. 上傳 hello 應用程式封裝 toohello 映像存放區
3. 註冊 hello 應用程式類型
4. 移除任何執行中的應用程式執行個體
5. 建立應用程式執行個體

在 Visual Studio 中，按下**F5**部署您的應用程式，並附加 hello 偵錯工具 tooall 應用程式執行個體。 您可以使用**Ctrl + F5** toodeploy 而不偵錯，或您的應用程式可以發佈 tooa 本機或遠端叢集使用 hello 發行設定檔。 如需詳細資訊，請參閱[使用 Visual Studio 發行應用程式 tooa 遠端叢集](service-fabric-publish-app-remote-cluster.md)。

### <a name="application-debug-mode"></a>應用程式偵錯模式
Visual Studio 提供屬性，稱為**應用程式偵錯模式**，這會控制所需的 Visual Studio toohandle 應用程式部署為偵錯的一部分。

#### <a name="tooset-hello-application-debug-mode-property"></a>tooset hello 應用程式偵錯模式屬性
1. Hello Service Fabric 應用程式的專案 (*.sfproj) 上快顯功能表上，選擇**屬性**(或按 hello **F4**索引鍵)。
2. 在 hello**屬性**視窗中，設定 hello**應用程式偵錯模式**屬性。

![設定應用程式偵錯模式屬性][debugmodeproperty]

#### <a name="application-debug-modes"></a>應用程式偵錯模式

1. **重新整理應用程式**這個模式可讓您 tooquickly 變更，並且偵錯程式碼和偵錯時編輯靜態網頁檔案的支援。 這種模式僅適用於您的本機開發叢集為 [1 個節點模式](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode)的情況。
2. **移除應用程式**原因 hello 應用程式 toobe hello 偵錯工作階段結束時移除。
3. **自動升級**hello 應用程式會繼續 toorun hello 偵錯工作階段結束時。 hello 下一個偵錯工作階段會視為 hello 部署升級。 hello 升級程序會保留您在先前的偵錯工作階段中輸入任何資料。
4. **保留應用程式**hello 時 hello hello 叢集中執行的應用程式會保留偵錯工作階段隨即結束。 在 hello 開頭 hello 下一個偵錯工作階段，將會移除 hello 應用程式。

如**自動升級**資料會保留以供套用 hello 的 Service Fabric 應用程式升級功能。 如需有關升級應用程式和如何在實際環境中執行升級的詳細資訊，請參閱 [Service Fabric 應用程式升級](service-fabric-application-upgrade.md)。

## <a name="add-a-service-tooyour-service-fabric-application"></a>新增服務 tooyour Service Fabric 應用程式
您可以加入新的服務 tooyour 應用程式 tooextend 其功能。  tooensure hello 服務隨附於您的應用程式封裝，加入 hello 服務透過 hello**新增 Fabric 服務...**功能表項目。

![新增 Service Fabric 服務][newservice]

選取 Service Fabric 專案類型 tooadd tooyour 應用程式，並指定 hello 服務的名稱。  請參閱[選擇您的服務的架構](service-fabric-choose-framework.md)toohelp 您決定哪一種服務類型 toouse。

![選取 Service Fabric 服務專案類型 tooadd tooyour 應用程式][addserviceproject]

hello 新服務會加入 tooyour 解決方案與現有應用程式封裝。 hello 服務參考和預設的服務執行個體將會加入的 toohello 應用程式資訊清單，導致 hello 服務 toobe 建立並啟動 hello 部署 hello 應用程式的下一次。

![加入 tooyour 應用程式資訊清單的 hello 新的服務][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a>封裝 Service Fabric 應用程式
toodeploy hello 應用程式和其服務 tooa 叢集，您會需要 toocreate 應用程式封裝。  hello 封裝組織 hello 應用程式資訊清單、 服務資訊清單，然後以特定配置其他必要的檔案。  Visual Studio 設定及管理 hello 套件 hello 'byok-kek-pkg' 目錄中的 hello 應用程式專案的資料夾中。  按一下**封裝**從 hello**應用程式**內容功能表建立或更新 hello 應用程式套件。

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a>使用 Cloud Explorer 移除應用程式和應用程式類型
您可以執行基本的叢集管理作業從 Visual Studio 中使用 Cloud Explorer，您可以從 hello 啟動**檢視**功能表。 例如，您可以在本機或遠端叢集上刪除應用程式和解除佈建應用程式類型。

![移除應用程式][removeapplication]

> [!TIP]
> 如需更豐富的叢集管理功能，請參閱 [使用 Service Fabric Explorer 視覺化叢集](service-fabric-visualizing-your-cluster.md)。
>
>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>後續步驟
* [Service Fabric 應用程式模型](service-fabric-application-model.md)
* [Service Fabric 應用程式部署](service-fabric-deploy-remove-applications.md)
* [管理多個環境的應用程式參數](service-fabric-manage-multiple-environment-app-configuration.md)
* [偵錯 Service Fabric 應用程式](service-fabric-debugging-your-application.md)
* [使用 Service Fabric 總管視覺化叢集](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png