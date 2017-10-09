---
title: "在 Linux 上的 Service Fabric aaaAzure |Microsoft 文件"
description: "Service Fabric 叢集支援 Linux 和 Java 中，這表示您將會無法 toodeploy 而且 Java 和 C# 中撰寫在 Linux 上的主機 Service Fabric 應用程式。"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 459afade-145d-4ee6-b72b-ddf380ccd1bf
ms.service: service-fabric
ms.devlang: Java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: SubramaR
ms.openlocfilehash: ca0e092b00faec560963c0d6cc379593d085f6a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-on-linux"></a>Linux 上的 Service Fabric
在 Linux 上的 Service Fabric hello 預覽可讓您 toobuild、 部署和管理 Linux 上的高可用性、 高擴充性應用程式，就如同在 Windows 上。 在 Linux 上的 Java 加法 tooC # (.NET Core) 中使用 hello Service Fabric 架構 （可靠的服務和 Reliable Actors）。  您也可以使用任何語言或架構來建置 [來賓可執行檔服務](service-fabric-deploy-existing-app.md) 。 此外，hello 預覽也支援協調 Docker 容器。 客體可執行檔或原生的 Service Fabric 服務，使用 hello Service Fabric 架構，可以執行 docker 容器。

在 Linux 上的 Service Fabric 這概念上相當 tooService Windows 上的網狀架構 （除了作業系統特性和程式設計語言支援）。 因此，大部分的我們[現有文件集](http://aka.ms/servicefabricdocs)適用於協助您熟悉 hello 技術。

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Service-Fabric-Linux-Preview/player]
>
>

## <a name="supported-operating-systems-and-programming-languages"></a>支援的作業系統和程式設計語言
有限的 hello 預覽支援 hello 建立一個方塊開發此外叢集在 Azure 中執行 Ubuntu Server 16.04 toomulti 機器叢集。 hello 預覽支援 hello Reliable Actors 和 hello Java 和 C# 中的可靠的無狀態服務架構新增 tooguest 可執行檔和協調 Docker 容器中。  

> [!NOTE]
> Linux 尚未支援 Reliable Collections。 不支援獨立單獨叢集 hello 預覽支援是-只有一個方塊和 Azure Linux 多電腦叢集。
>
>


## <a name="supported-tooling"></a>支援的工具
hello 預覽支援與透過 Service Fabric CLI hello 叢集之間的互動。 針對 Java 開發人員，透過 Linux 和 OSX 上支援的 Eclipse，就能與 Eclipse 和 Yeoman 整合。 hello OSX 整合會使用透過 vagrant hello 幕後 Linux VM。 C# 開發人員，與 Yeoman 整合提供 toogenerate 應用程式範本。

## <a name="next-steps"></a>後續步驟

* 讓您熟悉 hello [Reliable Actors](service-fabric-reliable-actors-introduction.md)和[可靠服務](service-fabric-reliable-services-introduction.md)程式設計架構
* [在 Linux 上準備您的開發環境](service-fabric-get-started-linux.md)
* [在 OSX 上準備您的開發環境](service-fabric-get-started-mac.md)
* [在 Linux 上建立第一個 Service Fabric Java 應用程式](service-fabric-create-your-first-linux-application-with-java.md)
* [使用 Jenkins 和 GitHub 設定 Service Fabric 連續整合和部署](service-fabric-cicd-your-linux-java-application-with-jenkins.md)
* [Service Fabric Windows/Linux 的差異](service-fabric-linux-windows-differences.md)
