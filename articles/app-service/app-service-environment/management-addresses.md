---
title: "aaaAzure App Service 環境管理位址"
description: "列出 hello 管理位址使用 toocommand App Service 環境"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: a7738a24-89ef-43d3-bff1-77f43d5a3952
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: b34b6266dc3a35915421b14bf34eddc07c2825c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-management-addresses"></a>App Service Environment 管理位址

hello 應用程式服務 Environment(ASE) 是 hello 的部署至 Azure 虛擬網路 (VNet) 中的子網路 Azure 應用程式服務。  hello ASE 必須能從存取 hello Azure 應用程式服務，讓您可以管理。  此 ASE 管理流量會周遊 hello 使用者控制網路。  來自 Azure App Service management 伺服器 toohello 公用 VIP hello ASE 與相關聯。  如需詳細資訊，在 hello ASE 網路功能相依性讀取[網路考量和 App Service 環境的 hello][networking]。  如需一般資訊 hello ASE 就可以開始[簡介 toohello App Service 環境][intro]。

本文件列出管理流量 toohello ASE 的 hello 來源 Ip。 您可以使用這些位址 toocreate 網路安全性群組 toolock 的向下連入流量，或視需要在路由表中使用它們。  toouse 需要 toouse 這項資訊：

* 列出所有地區的 hello IP 位址
* hello IP 位址您 ASE 部署到該相符項目 toohello 區域。

hello 連入的管理流量來自這些 IP 位址 tooports 454 和 455。

| 區域 | 位址 |
|--------|-----------|
| 所有區域 | 70.37.57.58, 157.55.208.185 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141 |
| 美國中南部和美國中北部 | 23.102.188.65, 191.236.154.88 |
| 澳大利亞東南部和澳大利亞東部 | 23.101.234.41, 104.210.90.65 |
| 美國西部和美國東部 | 104.45.227.37, 191.236.60.72 |
| 西歐和北歐 | 191.233.94.45, 191.237.222.191 |
| 美國中西部和美國西部 2 | 13.78.148.75, 13.66.225.188 |
| 美國中部和美國東部 2 | 104.43.165.73, 104.46.108.135 |
| 東亞和東南亞 | 23.99.115.5, 104.215.158.33 |
| 日本東部和日本西部 | 104.41.185.116, 191.239.104.48 |
| 加拿大中部和加拿大東部 | 40.85.230.101, 40.86.229.100 |
| 英國西部和英國南部 | 51.141.8.34, 51.140.185.75 |
| 韓國中部和韓國南部 | 52.231.200.177, 52.231.32.117 |
| 巴西南部和美國中南部| 104.41.46.178, 23.102.188.65 |
| 印度中部和印度南部 | 104.211.98.24, 104.211.225.66 |
| 印度西部和印度南部 | 104.211.160.229, 104.211.225.66 |


<!-- LINKS -->
[networking]: ./network-info.md
[intro]: ./intro.md
