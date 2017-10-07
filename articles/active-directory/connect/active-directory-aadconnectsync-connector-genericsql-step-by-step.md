---
title: "SQL 連接器的逐步 aaaGeneric 步驟 |Microsoft 文件"
description: "這篇文章會帶您透過簡單的 HR 系統逐步使用 hello 泛型 SQL 連接器。"
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 28c1cc60-24fd-4d0d-a36d-b4aba6de86e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b1b5f89ab588de6f92f173a7bc00f97180067669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-step-by-step"></a>一般 SQL 連接器的逐步解說
本主題是一份逐步解說指南。 它會建立簡單的範例 HR 資料庫，並用於匯入某些使用者和他們的群組成員資格。

## <a name="prepare-hello-sample-database"></a>準備 hello 範例資料庫
在伺服器上執行 SQL Server，執行 hello SQL 指令碼中找到[附錄 A](#appendix-a)。此指令碼會建立具有 hello 名稱 GSQLDEMO 範例資料庫。 hello 的 hello 物件模型會建立此圖中的資料庫類似：  
![物件模型](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)

也請建立您想要 toouse tooconnect toohello 資料庫使用者。 在本逐步解說中，會 hello 使用者呼叫 FABRIKAM\SQLUser，並位於 hello 網域中。

## <a name="create-hello-odbc-connection-file"></a>建立 hello ODBC 連接檔案
hello 泛型 SQL 連接器會使用 ODBC tooconnect toohello 遠端伺服器。 首先，我們需要 toocreate hello ODBC 連接資訊的檔案。

1. 在您的伺服器上啟動 hello ODBC 管理公用程式：  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. 選取 hello 索引標籤**檔案 DSN**。 按一下 [新增...] 。  
   ![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)
3. hello 鶈蜪驅動程式的運作精確，因此選取它，然後按一下 **下一步 >**。  
   ![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)
4. 指定 hello 檔案的名稱，例如**GenericSQL**。  
   ![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)
5. 按一下 [完成] 。  
   ![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)
6. 階段 tooconfigure hello 連接。 提供 hello 資料來源的良好的描述，並提供 hello hello 執行 SQL Server 的伺服器名稱。  
   ![ODBC5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. 選取如何使用 SQL tooauthenticate。 在此案例中，我們會使用 Windows 驗證。  
   ![ODBC6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. 提供的 hello 範例資料庫中的 hello 名稱**GSQLDEMO**。  
   ![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)
9. 將此畫面上的所有項目保留為預設值。 按一下 [完成] 。  
   ![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)
10. 按一下 所有項目是否正常運作，tooverify**測試資料來源**。  
    ![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)
11. 請確定 hello 測試不成功。  
    ![ODBC10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. 現在應該顯示在 檔案 DSN hello ODBC 組態檔。  
    ![ODBC11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

我們現在有 hello 檔案我們需要可以開始建立 hello 連接器。

## <a name="create-hello-generic-sql-connector"></a>建立 hello 泛型 SQL 連接器
1. 在 hello 同步處理服務管理員 UI 中，選取 **連接器**和**建立**。 選取 [一般 SQL (Microsoft)]  並為它提供描述性名稱。  
   ![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)
2. 尋找您建立 hello 前一節中的 hello DSN 檔案，並將它上傳 toohello 伺服器。 提供 hello 認證 tooconnect toohello 資料庫。  
   ![Connector2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. 在本逐步解說中，為方便起見，我們假設有兩個物件類型：**User** 和 **Group**。
   ![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)
4. toofind hello 屬性，我們想要藉由查看 hello 資料表本身 hello 連接器 toodetect 那些屬性。 因為**使用者**是保留的字在 SQL 中，我們需要 tooprovide 在方括號 []。  
   ![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)
5. 時間 toodefine hello 錨點屬性以及 hello DN 屬性。 如**使用者**，我們使用的 hello 兩個屬性的使用者名稱和 EmployeeID 的 hello 組合。 我們針對 **group**使用GroupName (在真實生活中並不實際，但對本逐步解說而言，它是可行的)。
   ![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)
6. 並非所有屬性類型都可以在 SQL 資料庫中偵測到。 特別是無法 hello 參考屬性的型別。 Hello 群組物件類型，我們需要 toochange hello OwnerID 和 tooreference memberid 的值。  
   ![Connector6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. hello 我們選取屬性 hello 上一個步驟中的參考屬性需要 hello 這些值所參考的物件類型。 在此案例中 hello 使用者物件類型。  
   ![Connector7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. 在 hello 全域參數 頁面上，選取 **浮水印**做為 hello 差異策略。 也在 hello 日期/時間格式鍵入**yyyy MM dd hh: mm:**。
   ![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)
9. 在 hello**設定分割和階層**頁面上，選取這兩種物件類型。
   ![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)
10. 在 hello**選取物件類型**和**選取屬性**，選取物件類型和所有屬性。 在 hello**設定錨點**頁面上，按一下**完成**。

## <a name="create-run-profiles"></a>建立執行設定檔
1. 在 hello 同步處理服務管理員 UI 中，選取 **連接器**，和**設定執行設定檔**。 按一下 [新增設定檔]。 我們會從**完整匯入**開始。  
   ![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)
2. 選取 hello 類型**完整匯入 （只有階段）**。  
   ![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)
3. 選取資料分割，hello**物件 = 使用者**。  
   ![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)
4. 選取 [資料表] 並輸入 [USERS]。 捲動 toohello 多重值的物件類型 區段中，然後輸入 hello 資料，如 hello 下列圖片所示。 選取**完成**toosave hello 步驟。  
   ![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)  
   ![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)  
5. 選取 [新增步驟] 。 這次選取 [OBJECT=Group] 。 在 hello 最後一個頁面上，使用 hello 設定如 hello 下列圖片所示。 按一下 [完成] 。  
   ![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)  
   ![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)  
6. 選用︰如果您想要，您可以設定其他的執行設定檔。 這個逐步解說中，會使用 hello 完整匯入。
7. 按一下**確定**toofinish 變更執行設定檔。

## <a name="add-some-test-data-and-test-hello-import"></a>加入一些測試資料和測試 hello 匯入
在範例資料庫中填入部分測試資料。 當您準備好時，選取 [執行] 和 [完整匯入]。

以下是具有兩個電話號碼的使用者以及含有一些成員的群組。  
![cs1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![cs2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a>附錄 A
**SQL 指令碼 toocreate hello 範例資料庫**

```SQL
---Creating hello Database---------
Create Database GSQLDEMO
Go
-------Using hello Database-----------
Use [GSQLDEMO]
Go
-------------------------------------
USE [GSQLDEMO]
GO
/****** Object:  Table [dbo].[GroupMembers]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GroupMembers](
    [MemberID] [int] NOT NULL,
    [Group_ID] [int] NOT NULL
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[GROUPS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GROUPS](
    [GroupID] [int] NOT NULL,
    [GROUPNAME] [nvarchar](200) NOT NULL,
    [DESCRIPTION] [nvarchar](200) NULL,
    [WATERMARK] [datetime] NULL,
    [OwnerID] [int] NULL,
PRIMARY KEY CLUSTERED
(
    [GroupID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[USERPHONE]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
SET ANSI_PADDING ON
GO
CREATE TABLE [dbo].[USERPHONE](
    [USER_ID] [int] NULL,
    [Phone] [varchar](20) NULL
) ON [PRIMARY]

GO
SET ANSI_PADDING OFF
GO
/****** Object:  Table [dbo].[USERS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[USERS](
    [USERID] [int] NOT NULL,
    [USERNAME] [nvarchar](200) NOT NULL,
    [FirstName] [nvarchar](100) NULL,
    [LastName] [nvarchar](100) NULL,
    [DisplayName] [nvarchar](100) NULL,
    [ACCOUNTDISABLED] [bit] NULL,
    [EMPLOYEEID] [int] NOT NULL,
    [WATERMARK] [datetime] NULL,
PRIMARY KEY CLUSTERED
(
    [USERID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_GROUPS] FOREIGN KEY([Group_ID])
REFERENCES [dbo].[GROUPS] ([GroupID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_GROUPS]
GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_USERS] FOREIGN KEY([MemberID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_USERS]
GO
ALTER TABLE [dbo].[GROUPS]  WITH CHECK ADD  CONSTRAINT [FK_GROUPS_USERS] FOREIGN KEY([OwnerID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GROUPS] CHECK CONSTRAINT [FK_GROUPS_USERS]
GO
ALTER TABLE [dbo].[USERPHONE]  WITH CHECK ADD  CONSTRAINT [FK_USERPHONE_USER] FOREIGN KEY([USER_ID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[USERPHONE] CHECK CONSTRAINT [FK_USERPHONE_USER]
GO
```
