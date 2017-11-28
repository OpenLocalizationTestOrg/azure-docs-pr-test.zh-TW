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
# <a name="generic-sql-connector-step-by-step"></a><span data-ttu-id="dbdc7-103">一般 SQL 連接器的逐步解說</span><span class="sxs-lookup"><span data-stu-id="dbdc7-103">Generic SQL Connector step-by-step</span></span>
<span data-ttu-id="dbdc7-104">本主題是一份逐步解說指南。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-104">This topic is a step-by-step guide.</span></span> <span data-ttu-id="dbdc7-105">它會建立簡單的範例 HR 資料庫，並用於匯入某些使用者和他們的群組成員資格。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-105">It creates a simple sample HR database and use it for importing some users and their group membership.</span></span>

## <a name="prepare-hello-sample-database"></a><span data-ttu-id="dbdc7-106">準備 hello 範例資料庫</span><span class="sxs-lookup"><span data-stu-id="dbdc7-106">Prepare hello sample database</span></span>
<span data-ttu-id="dbdc7-107">在伺服器上執行 SQL Server，執行 hello SQL 指令碼中找到[附錄 A](#appendix-a)。此指令碼會建立具有 hello 名稱 GSQLDEMO 範例資料庫。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-107">On a server running SQL Server, run hello SQL script found in [Appendix A](#appendix-a). This script creates a sample database with hello name GSQLDEMO.</span></span> <span data-ttu-id="dbdc7-108">hello 的 hello 物件模型會建立此圖中的資料庫類似：</span><span class="sxs-lookup"><span data-stu-id="dbdc7-108">hello object model for hello created database looks like this picture:</span></span>  
<span data-ttu-id="dbdc7-109">![物件模型](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span><span class="sxs-lookup"><span data-stu-id="dbdc7-109">![Object Model](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span></span>

<span data-ttu-id="dbdc7-110">也請建立您想要 toouse tooconnect toohello 資料庫使用者。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-110">Also create a user you want toouse tooconnect toohello database.</span></span> <span data-ttu-id="dbdc7-111">在本逐步解說中，會 hello 使用者呼叫 FABRIKAM\SQLUser，並位於 hello 網域中。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-111">In this walkthrough, hello user is called FABRIKAM\SQLUser and located in hello domain.</span></span>

## <a name="create-hello-odbc-connection-file"></a><span data-ttu-id="dbdc7-112">建立 hello ODBC 連接檔案</span><span class="sxs-lookup"><span data-stu-id="dbdc7-112">Create hello ODBC connection file</span></span>
<span data-ttu-id="dbdc7-113">hello 泛型 SQL 連接器會使用 ODBC tooconnect toohello 遠端伺服器。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-113">hello Generic SQL Connector is using ODBC tooconnect toohello remote server.</span></span> <span data-ttu-id="dbdc7-114">首先，我們需要 toocreate hello ODBC 連接資訊的檔案。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-114">First we need toocreate a file with hello ODBC connection information.</span></span>

1. <span data-ttu-id="dbdc7-115">在您的伺服器上啟動 hello ODBC 管理公用程式：</span><span class="sxs-lookup"><span data-stu-id="dbdc7-115">Start hello ODBC management utility on your server:</span></span>  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. <span data-ttu-id="dbdc7-117">選取 hello 索引標籤**檔案 DSN**。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-117">Select hello tab **File DSN**.</span></span> <span data-ttu-id="dbdc7-118">按一下 [新增...] 。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-118">Click **Add...**.</span></span>  
   <span data-ttu-id="dbdc7-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span><span class="sxs-lookup"><span data-stu-id="dbdc7-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span></span>
3. <span data-ttu-id="dbdc7-120">hello 鶈蜪驅動程式的運作精確，因此選取它，然後按一下 **下一步 >**。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-120">hello out-of-box driver works fine, so select it and click **Next>**.</span></span>  
   <span data-ttu-id="dbdc7-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span><span class="sxs-lookup"><span data-stu-id="dbdc7-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span></span>
4. <span data-ttu-id="dbdc7-122">指定 hello 檔案的名稱，例如**GenericSQL**。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-122">Give hello file a name, such as **GenericSQL**.</span></span>  
   <span data-ttu-id="dbdc7-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span><span class="sxs-lookup"><span data-stu-id="dbdc7-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span></span>
5. <span data-ttu-id="dbdc7-124">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-124">Click **Finish**.</span></span>  
   <span data-ttu-id="dbdc7-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span><span class="sxs-lookup"><span data-stu-id="dbdc7-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span></span>
6. <span data-ttu-id="dbdc7-126">階段 tooconfigure hello 連接。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-126">Time tooconfigure hello connection.</span></span> <span data-ttu-id="dbdc7-127">提供 hello 資料來源的良好的描述，並提供 hello hello 執行 SQL Server 的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-127">Give hello data source a good description and provide hello name of hello server running SQL Server.</span></span>  
   ![ODBC5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. <span data-ttu-id="dbdc7-129">選取如何使用 SQL tooauthenticate。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-129">Select how tooauthenticate with SQL.</span></span> <span data-ttu-id="dbdc7-130">在此案例中，我們會使用 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-130">In this case, we use Windows Authentication.</span></span>  
   ![ODBC6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. <span data-ttu-id="dbdc7-132">提供的 hello 範例資料庫中的 hello 名稱**GSQLDEMO**。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-132">Provide hello name of hello sample database, **GSQLDEMO**.</span></span>  
   <span data-ttu-id="dbdc7-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span><span class="sxs-lookup"><span data-stu-id="dbdc7-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span></span>
9. <span data-ttu-id="dbdc7-134">將此畫面上的所有項目保留為預設值。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-134">Keep everything default on this screen.</span></span> <span data-ttu-id="dbdc7-135">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-135">Click **Finish**.</span></span>  
   <span data-ttu-id="dbdc7-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span><span class="sxs-lookup"><span data-stu-id="dbdc7-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span></span>
10. <span data-ttu-id="dbdc7-137">按一下 所有項目是否正常運作，tooverify**測試資料來源**。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-137">tooverify everything is working as expected, click **Test Data Source**.</span></span>  
    <span data-ttu-id="dbdc7-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span><span class="sxs-lookup"><span data-stu-id="dbdc7-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span></span>
11. <span data-ttu-id="dbdc7-139">請確定 hello 測試不成功。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-139">Make sure hello test is successful.</span></span>  
    ![ODBC10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. <span data-ttu-id="dbdc7-141">現在應該顯示在 檔案 DSN hello ODBC 組態檔。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-141">hello ODBC configuration file should now be visible in File DSN.</span></span>  
    ![ODBC11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

<span data-ttu-id="dbdc7-143">我們現在有 hello 檔案我們需要可以開始建立 hello 連接器。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-143">We now have hello file we need and can start creating hello Connector.</span></span>

## <a name="create-hello-generic-sql-connector"></a><span data-ttu-id="dbdc7-144">建立 hello 泛型 SQL 連接器</span><span class="sxs-lookup"><span data-stu-id="dbdc7-144">Create hello Generic SQL Connector</span></span>
1. <span data-ttu-id="dbdc7-145">在 hello 同步處理服務管理員 UI 中，選取 **連接器**和**建立**。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-145">In hello Synchronization Service Manager UI, select **Connectors** and **Create**.</span></span> <span data-ttu-id="dbdc7-146">選取 [一般 SQL (Microsoft)]  並為它提供描述性名稱。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-146">Select **Generic SQL (Microsoft)** and give it a descriptive name.</span></span>  
   <span data-ttu-id="dbdc7-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span><span class="sxs-lookup"><span data-stu-id="dbdc7-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span></span>
2. <span data-ttu-id="dbdc7-148">尋找您建立 hello 前一節中的 hello DSN 檔案，並將它上傳 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-148">Find hello DSN file you created in hello previous section and upload it toohello server.</span></span> <span data-ttu-id="dbdc7-149">提供 hello 認證 tooconnect toohello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-149">Provide hello credentials tooconnect toohello database.</span></span>  
   ![Connector2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. <span data-ttu-id="dbdc7-151">在本逐步解說中，為方便起見，我們假設有兩個物件類型：**User** 和 **Group**。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-151">In this walkthrough, we are making it easy for us and say that there are two object types, **User** and **Group**.</span></span>
   <span data-ttu-id="dbdc7-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span><span class="sxs-lookup"><span data-stu-id="dbdc7-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span></span>
4. <span data-ttu-id="dbdc7-153">toofind hello 屬性，我們想要藉由查看 hello 資料表本身 hello 連接器 toodetect 那些屬性。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-153">toofind hello attributes, we want hello Connector toodetect those attributes by looking at hello table itself.</span></span> <span data-ttu-id="dbdc7-154">因為**使用者**是保留的字在 SQL 中，我們需要 tooprovide 在方括號 []。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-154">Since **Users** is a reserved word in SQL, we need tooprovide it in square brackets [ ].</span></span>  
   <span data-ttu-id="dbdc7-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span><span class="sxs-lookup"><span data-stu-id="dbdc7-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span></span>
5. <span data-ttu-id="dbdc7-156">時間 toodefine hello 錨點屬性以及 hello DN 屬性。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-156">Time toodefine hello anchor attribute and hello DN attribute.</span></span> <span data-ttu-id="dbdc7-157">如**使用者**，我們使用的 hello 兩個屬性的使用者名稱和 EmployeeID 的 hello 組合。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-157">For **Users**, we use hello combination of hello two attributes username and EmployeeID.</span></span> <span data-ttu-id="dbdc7-158">我們針對 **group**使用GroupName (在真實生活中並不實際，但對本逐步解說而言，它是可行的)。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-158">For **group**, we use GroupName (not realistic in real-life, but for this walkthrough it works).</span></span>
   <span data-ttu-id="dbdc7-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span><span class="sxs-lookup"><span data-stu-id="dbdc7-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span></span>
6. <span data-ttu-id="dbdc7-160">並非所有屬性類型都可以在 SQL 資料庫中偵測到。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-160">Not all attribute types can be detected in a SQL database.</span></span> <span data-ttu-id="dbdc7-161">特別是無法 hello 參考屬性的型別。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-161">hello reference attribute type in particular cannot.</span></span> <span data-ttu-id="dbdc7-162">Hello 群組物件類型，我們需要 toochange hello OwnerID 和 tooreference memberid 的值。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-162">For hello group object type, we need toochange hello OwnerID and MemberID tooreference.</span></span>  
   ![Connector6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. <span data-ttu-id="dbdc7-164">hello 我們選取屬性 hello 上一個步驟中的參考屬性需要 hello 這些值所參考的物件類型。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-164">hello attributes we selected as reference attributes in hello previous step require hello object type these values are a reference to.</span></span> <span data-ttu-id="dbdc7-165">在此案例中 hello 使用者物件類型。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-165">In our case, hello User object type.</span></span>  
   ![Connector7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. <span data-ttu-id="dbdc7-167">在 hello 全域參數 頁面上，選取 **浮水印**做為 hello 差異策略。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-167">On hello Global Parameters page, select **Watermark** as hello delta strategy.</span></span> <span data-ttu-id="dbdc7-168">也在 hello 日期/時間格式鍵入**yyyy MM dd hh: mm:**。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-168">Also type in hello date/time format **yyyy-MM-dd HH:mm:ss**.</span></span>
   <span data-ttu-id="dbdc7-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span><span class="sxs-lookup"><span data-stu-id="dbdc7-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span></span>
9. <span data-ttu-id="dbdc7-170">在 hello**設定分割和階層**頁面上，選取這兩種物件類型。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-170">On hello **Configure Partitions and Hierarchies** page, select both object types.</span></span>
   <span data-ttu-id="dbdc7-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span><span class="sxs-lookup"><span data-stu-id="dbdc7-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span></span>
10. <span data-ttu-id="dbdc7-172">在 hello**選取物件類型**和**選取屬性**，選取物件類型和所有屬性。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-172">On hello **Select Object Types** and **Select Attributes**, select both object types and all attributes.</span></span> <span data-ttu-id="dbdc7-173">在 hello**設定錨點**頁面上，按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-173">On hello **Configure Anchors** page, click **Finish**.</span></span>

## <a name="create-run-profiles"></a><span data-ttu-id="dbdc7-174">建立執行設定檔</span><span class="sxs-lookup"><span data-stu-id="dbdc7-174">Create Run Profiles</span></span>
1. <span data-ttu-id="dbdc7-175">在 hello 同步處理服務管理員 UI 中，選取 **連接器**，和**設定執行設定檔**。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-175">In hello Synchronization Service Manager UI, select **Connectors**, and **Configure Run Profiles**.</span></span> <span data-ttu-id="dbdc7-176">按一下 [新增設定檔]。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-176">Click **New Profile**.</span></span> <span data-ttu-id="dbdc7-177">我們會從**完整匯入**開始。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-177">We start with **Full Import**.</span></span>  
   <span data-ttu-id="dbdc7-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span><span class="sxs-lookup"><span data-stu-id="dbdc7-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span></span>
2. <span data-ttu-id="dbdc7-179">選取 hello 類型**完整匯入 （只有階段）**。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-179">Select hello type **Full Import (Stage Only)**.</span></span>  
   <span data-ttu-id="dbdc7-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span><span class="sxs-lookup"><span data-stu-id="dbdc7-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span></span>
3. <span data-ttu-id="dbdc7-181">選取資料分割，hello**物件 = 使用者**。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-181">Select hello partition **OBJECT=User**.</span></span>  
   <span data-ttu-id="dbdc7-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span><span class="sxs-lookup"><span data-stu-id="dbdc7-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span></span>
4. <span data-ttu-id="dbdc7-183">選取 [資料表] 並輸入 [USERS]。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-183">Select **Table** and type **[USERS]**.</span></span> <span data-ttu-id="dbdc7-184">捲動 toohello 多重值的物件類型 區段中，然後輸入 hello 資料，如 hello 下列圖片所示。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-184">Scroll down toohello multi-valued object type section and enter hello data as in hello following picture.</span></span> <span data-ttu-id="dbdc7-185">選取**完成**toosave hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-185">Select **Finish** toosave hello step.</span></span>  
   <span data-ttu-id="dbdc7-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span><span class="sxs-lookup"><span data-stu-id="dbdc7-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span></span>  
   <span data-ttu-id="dbdc7-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span><span class="sxs-lookup"><span data-stu-id="dbdc7-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span></span>  
5. <span data-ttu-id="dbdc7-188">選取 [新增步驟] 。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-188">Select **New Step**.</span></span> <span data-ttu-id="dbdc7-189">這次選取 [OBJECT=Group] 。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-189">This time, select **OBJECT=Group**.</span></span> <span data-ttu-id="dbdc7-190">在 hello 最後一個頁面上，使用 hello 設定如 hello 下列圖片所示。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-190">On hello last page, use hello configuration as in hello following picture.</span></span> <span data-ttu-id="dbdc7-191">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-191">Click **Finish**.</span></span>  
   <span data-ttu-id="dbdc7-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span><span class="sxs-lookup"><span data-stu-id="dbdc7-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span></span>  
   <span data-ttu-id="dbdc7-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span><span class="sxs-lookup"><span data-stu-id="dbdc7-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span></span>  
6. <span data-ttu-id="dbdc7-194">選用︰如果您想要，您可以設定其他的執行設定檔。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-194">Optional: If you want to, you can configure additional run profiles.</span></span> <span data-ttu-id="dbdc7-195">這個逐步解說中，會使用 hello 完整匯入。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-195">For this walkthrough, only hello Full Import is used.</span></span>
7. <span data-ttu-id="dbdc7-196">按一下**確定**toofinish 變更執行設定檔。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-196">Click **OK** toofinish changing run profiles.</span></span>

## <a name="add-some-test-data-and-test-hello-import"></a><span data-ttu-id="dbdc7-197">加入一些測試資料和測試 hello 匯入</span><span class="sxs-lookup"><span data-stu-id="dbdc7-197">Add some test data and test hello import</span></span>
<span data-ttu-id="dbdc7-198">在範例資料庫中填入部分測試資料。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-198">Fill out some test data in your sample database.</span></span> <span data-ttu-id="dbdc7-199">當您準備好時，選取 [執行] 和 [完整匯入]。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-199">When you are ready, select **Run** and **Full import**.</span></span>

<span data-ttu-id="dbdc7-200">以下是具有兩個電話號碼的使用者以及含有一些成員的群組。</span><span class="sxs-lookup"><span data-stu-id="dbdc7-200">Here is a user with two phone numbers and a group with some members.</span></span>  
![cs1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![cs2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a><span data-ttu-id="dbdc7-203">附錄 A</span><span class="sxs-lookup"><span data-stu-id="dbdc7-203">Appendix A</span></span>
<span data-ttu-id="dbdc7-204">**SQL 指令碼 toocreate hello 範例資料庫**</span><span class="sxs-lookup"><span data-stu-id="dbdc7-204">**SQL script toocreate hello sample database**</span></span>

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
