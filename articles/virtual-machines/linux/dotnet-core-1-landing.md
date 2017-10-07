---
title: "aaaAzure Linux 虛擬機器 DotNet 核心教學課程 1 |Microsoft 文件"
description: "Azure 虛擬機器 DotNet 核心教學課程"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: b3652e86-0c44-4ac9-8cd1-27abdeaea4d4
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7e6f047197336de1e93c50413b6eabb718230bc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automating-application-deployments-toolinux-virtual-machines"></a>自動化應用程式部署 tooLinux 虛擬機器 

這個系列包含四個部分，詳細說明了如何使用 Azure Resource Manager 範本來部署及設定 Azure 資源和應用程式。 本系列的範例範本部署和 hello 檢查部署範本。 本系列的 hello 目標是 tooeducate hello Azure 資源，之間的關聯性，並 tooprovide 交給上部署完全整合的 Azure 資源管理員範本的經驗。 本文件假設您對 Azure Resource Manager 有基本程度的認識，開始進行本教學課程之前，請讓自己熟悉 Azure Resource Manager 的基本概念。 

## <a name="music-store-application"></a>音樂市集應用程式
hello 用於這一系列的範例是.Net Core 應用程式在模擬音樂商店購買體驗。 此應用程式可以是已部署的 tooeither Linux 或 Windows 的虛擬系統，同時已建立部署的範例。 hello 應用程式包含 web 應用程式和 SQL 資料庫。 在閱讀本系列文章 hello 之前, 部署 hello 應用程式使用此頁面上找到的 hello 部署按鈕。 完整部署時，hello 應用程式 / Azure 架構看起來像下列圖表中的 hello。 

hello 音樂存放區 Resource Manager 範本可以在這裡，找到[音樂存放區 Linux 範本](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db)

![音樂市集應用程式](./media/dotnet-core-1-landing/music-store.png)

每個元件，包括 hello JSON 會檢查下列四個發行項的 hello 範本產生關聯。

* [**應用程式架構**](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) – 應用程式元件，例如網站和資料庫需要 toobe 裝載於 Azure 的電腦資源，例如虛擬機器和 Azure SQL 資料庫。 本文件逐步解說對應計算需要、 tooAzure 資源，以及部署與 Azure 資源管理員範本，這些資源。 
* [**存取與安全性**](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) – 裝載在 Azure 中的應用程式，時，需要 tooconsider hello 應用程式存取時，以及如何在不同的應用程式元件彼此存取。 本文件詳述提供和保護網際網路存取 tooan 應用程式和應用程式元件之間的存取權。
* [**可用性和延展性**](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) – 延展和可用性，請參閱 toohello 基礎結構停機期間執行的應用程式的能力 toostay 和 hello 能力 tooscale 計算資源 toomeet 應用程式的需要。 此文件詳細資料 hello 元件需要的 toodeploy 負載平衡和高可用性的應用程式。
* [**應用程式部署**](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -時必須考量部署應用程式到 Azure 虛擬機器，根據哪個 hello hello 虛擬機器安裝應用程式二進位檔的 hello 方法。 此文件詳細說明如何使用「Azure 虛擬機器自訂指令碼擴充功能」來自動安裝應用程式。

hello 開發 Azure 資源管理員範本時的目標是 tooautomate hello 部署 Azure 基礎結構和 hello 安裝和任何的設定應用程式裝載於 Azure 基礎結構。 仔細閱讀這些文章將可獲得這項體驗的範例解說。

## <a name="deploy-hello-music-store-application"></a>部署 hello 音樂市集應用程式
hello Music Store 應用程式可以使用這個按鈕進行部署。

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FMicrosoft%2Fdotnet-core-sample-templates%2Fmaster%2Fdotnet-core-music-linux%2Fazuredeploy.json" target="_blank"> <img src="http://azuredeploy.net/deploybutton.png"/>
</a>

hello Azure Resource Manager 範本需要 hello 下列參數值。

| 參數名稱 | 說明 |
| --- | --- |
| SSHKEYDATA |Toosecure 存取 toohello 虛擬機器使用 SSH 金鑰的資料。 如需有關建立 SSH 金鑰組的資訊，請參閱[在 Azure 中為 Linux VM 建立 SSH 金鑰](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 |
| ADMINUSERNAME |使用 hello 虛擬機器和 hello Azure SQL Database 的系統管理員使用者名稱。 |
| SQLADMINPASSWORD |適用於 hello Azure SQL Database 的密碼。 |
| NUMBEROFINSTANCES |hello 建立的虛擬機器 toobe 數目。 每個這些虛擬機器主機 hello Music Store web 應用程式，以及所有流量是負載平衡它們。 |
| PUBLICIPADDRESSDNSNAME |Hello 公用 IP 位址相關聯的全域唯一 DNS 名稱。 |

Hello 範本部署完成後，瀏覽的 toohello 公用 IP 位址使用任何網際網路瀏覽器。 hello.Net Core 音樂站台將會出現。

## <a name="next-steps"></a>後續步驟
<hr>

[步驟 1 - 使用 Azure Resource Manager 範本的應用程式架構](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[步驟 2 - Azure Resource Manager 範本中的存取和安全性](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[步驟 3 - Azure Resource Manager 範本中的可用性和規模](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[步驟 4 - 使用 Azure Resource Manager 範本進行應用程式部署](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

