---
title: "Microsoft® Smooth Streaming Client Porting Kit aaaLicensing"
description: "深入了解如何 toolicensing hello Microsoft® Smooth Streaming Client Porting Kit。"
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: e3b488e7-8428-4c10-a072-eb3af46c82ad
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: xpouyat
ms.openlocfilehash: 56c3dccda73dd02207bb4dbe8109ba6fda917a6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-microsoft-smooth-streaming-client-porting-kit"></a>Licensing Microsoft® Smooth Streaming Client Porting Kit
## <a name="overview"></a>概觀
Microsoft Smooth Streaming Client Porting Kit (**SSPK**縮寫) 是最佳化的 toohelp 內嵌裝置製造商、 纜線和行動業者、 內容服務提供者、 手持式 Smooth Streaming 用戶端實作製造商、 獨立軟體廠商 (Isv) 和方案提供者 toocreate 產品和服務的串流 Smooth Streaming 格式的彈性串流內容。 SSPK 是 Smooth Streaming 的用戶端 hello 願 tooany 裝置的平台都可移植的裝置和平台獨立實作。 

包含在下面是高層級架構和 IIS Smooth Streaming Porting Kit 方塊是由 Microsoft 提供的 hello Smooth Streaming 的用戶端實作，並包含 Smooth Streaming 內容的播放的所有 hello 核心邏輯。 然而，特定裝置或平台的合作夥伴可藉由實作適當的介面來移植該架構。 

![SSPK](./media/media-services-sspk/sspk-arch.png)

## <a name="description"></a>說明
SSPK 是根據可提供絕佳商業價值的條款授權。 SSPK 授權提供與 hello 業界：

* Smooth Streaming Porting Kit 的 C++ 原始碼 
  * 實作 Smooth Streaming 用戶端功能
  * 新增格式剖析、啟發學習法、緩衝處理邏輯等等
* 播放器應用程式 API 
  * 可與媒體播放器應用程式互動的程式設計介面
* 平台抽象層 (PAL) 介面 
  * 程式設計介面的互動 hello 作業系統 （執行緒、 通訊端）
* 硬體抽象層 (HAL) 介面 
  * 用於與硬體 A/V 解碼器 (解碼、轉譯) 互動的程式設計介面
* 數位版權管理 (DRM) 介面 
  * 處理 DRM 透過 hello DRM 抽象層 (DAL) 的程式設計介面
  * Microsoft PlayReady Porting Kit 個別出貨，但可透過這個介面整合。 如需 Microsoft PlayReady Device 授權的詳細資訊，請按一下 [這裡](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl)。
* 實作範例 
  * 適用於 Linux 的 PAL 實作範例
  * 適用於 GStreamer 的 HAL 實作範例

## <a name="licensing-options"></a>授權選項
Microsoft Smooth Streaming Client Porting Kit 兩個不同的授權合約下進行可用 toolicensees： 一個用於開發 Smooth Streaming 用戶端暫時產品和另一個用於散發 Smooth Streaming 用戶端最終產品 tooend 使用者。

* 晶片組製造商、 系統整合者，或獨立軟體廠商 (Isv) 要求來源的程式碼移植套件 toodevelop 暫時產品 Microsoft Smooth Streaming Client Porting Kit**暫時產品授權**應該執行。
* 如裝置製造商或 Smooth Streaming 用戶端最終產品 tooend 對於使用者而言，需要散布權利 Isv hello Microsoft Smooth Streaming Client Porting Kit**最終產品授權**應該執行。

### <a name="microsoft-smooth-streaming-client-porting-kit-interim-product-license"></a>Microsoft Smooth Streaming Client Porting Kit 中期產品授權
依據本授權，Microsoft 提供 Smooth Streaming Client Porting Kit hello 必要智慧財產的權限 toodevelop 及散發 Smooth Streaming 用戶端暫時產品 tooother Smooth Streaming Client Porting Kit 裝置被授權人的將 Smooth Streaming 用戶端最後一個產品。

#### <a name="fee-structure"></a>免費結構
美國 $50,000 單次許可費用提供存取 toohello Smooth Streaming Client Porting Kit。 

### <a name="microsoft-smooth-streaming-client-porting-kit-final-product-license"></a>Microsoft Smooth Streaming Client Porting Kit 最終產品授權
依據本授權，Microsoft 會提供所有必要的智慧財產的權限 tooreceive Smooth Streaming 用戶端暫時產品與其他的 Smooth Streaming Client Porting Kit 人均 toodistribute 公司品牌 Smooth Streaming 用戶端最後產品 tooend 使用者。

#### <a name="fee-structure"></a>免費結構
hello Smooth Streaming 用戶端最終產品提供獲微軟授權使用模型做為下：

* 送交的每一裝置實作為 $0.10 美元
* hello 獲微軟授權使用的上限為 50000 每年
* 每年前 10,000 個裝置實作不需權利金 

## <a name="licensing-procedure-and-sspk-access"></a>授權程序和 SSPK 存取
有關所有授權查詢，請寄送電子郵件至 [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) 。

hello [SSPK 發佈入口網站](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/)是可存取 tooregistered 暫時被授權人。

過渡期間和最終 SSPK 被授權人可以送出技術問題太[smoothpk@microsoft.com](mailto:smoothpk@microsoft.com)。

## <a name="microsoft-smooth-streaming-client-interim-product-agreement-licensees"></a>Microsoft Smooth Streaming 用戶端中期產品合約被授權者
* Adroit Business Solutions, Inc
* Advanced Digital Broadcast SA
* AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.
* Albis Technologies Ltd.
* Alticast Corporation
* Amazon Digital Services, Inc.
* Arion Technology, Inc.
* AVC Multimedia Software Co., Ltd.
* Cavium, Inc.
* EchoStar Purchasing Corporation
* Enseo, Inc.
* Fluendo S.A.
* HANDAN BroadInfoCom Co., Ltd.
* Infomir GMBH
* Irdeto USA Inc.
* iWEDIA S.A. 
* Liberty Global Services BV
* MediaTek Inc.
* MStar Co, Ltd
* Nintendo Co., Ltd.
* OpenTV, Inc.
* Saffron Digital Limited
* Sichuan Changhong Electric Co., Ltd
* SoftAtHome
* 索尼公司
* Tatung Technology Inc.
* TCL Technoly Electronics (Huizhou) Co., Ltd.
* Top Victory Investments, Ltd.
* Vestel Elektronik Sanayi ve Ticaret A.S.
* VisualOn, Inc.
* ZTE Corporation

## <a name="microsoft-smooth-streaming-client-final-product-agreement-licensees"></a>Microsoft Smooth Streaming 用戶端最終產品合約被授權者
* Advanced Digital Broadcast SA
* AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.
* Albis Technologies Ltd.
* Amazon Digital Services, Inc.
* AmTRAN Technology Co., Ltd.
* Arcadyan Technology Corporation
* Arion Technology, Inc.
* ATMACA ELEKTRONİK SAN. VE TİC. A.Ş
* British Sky Broadcasting Limited
* CastPal Technology Inc., Shenzhen
* Compal Electronics, Inc.
* Dongguan Digital AV Technology Corp., Ltd.
* EchoStar Purchasing Corporation
* Enseo, Inc.
* Filmflex Movies Limited
* Fluendo S.A.
* Gibson Innovations Limited
* Haier Information Applicantion S.R.L
* HANDAN BroadInfoCom Co., Ltd.
* Hisense International Co., Ltd. 
* Homecast Co.,Ltd
* Hon Hai Precision Industry Co., Ltd.
* Infomir GMBH
* Kaonmedia Co., Ltd.
* KDDI Corporation
* Nintendo Co., Ltd.
* Orange SA
* Saffron Digital Limited
* Sagemcom Broadband SAS
* Shenzhen Coship Electronics CO., LTD
* Shenzhen Jiuzhou Electric Co.,Ltd
* Shenzhen Skyworth Digital Technology Co., Ltd
* Sichuan Changhong Electric Co., Ltd.
* 致振企業股份有限公司
* Sky Deutschland Fernsehen GmbH & Co. KG
* SmarDTV S.A.
* SoftAtHome
* 索尼公司
* TCL Overseas Marketing (Macao Commercial Offshore) Limited
* Technicolor Delivery Technologies, SAS
* Tongfang Global Ltd.
* Top Victory Investments, Ltd.
* Toshiba Lifestyle Products & Services Corporation
* Universal Media Corporation /Slovakia/ s.r.o.
* VIZIO, Inc.
* Wistron Corporation
* ZTE Corporation


## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

