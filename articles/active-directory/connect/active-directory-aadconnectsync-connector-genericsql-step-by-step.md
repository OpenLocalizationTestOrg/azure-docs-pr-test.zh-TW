---
title: "一般 SQL 連接器的逐步解說 | Microsoft Docs"
description: "本文會帶領您使用一般 SQL 連接器逐步設定簡單的 HR 系統。"
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
ms.openlocfilehash: 3fdc1b405b95180d031aa4ad45b406f7fc149d8f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="generic-sql-connector-step-by-step"></a><span data-ttu-id="65f7f-103">一般 SQL 連接器的逐步解說</span><span class="sxs-lookup"><span data-stu-id="65f7f-103">Generic SQL Connector step-by-step</span></span>
<span data-ttu-id="65f7f-104">本主題是一份逐步解說指南。</span><span class="sxs-lookup"><span data-stu-id="65f7f-104">This topic is a step-by-step guide.</span></span> <span data-ttu-id="65f7f-105">它會建立簡單的範例 HR 資料庫，並用於匯入某些使用者和他們的群組成員資格。</span><span class="sxs-lookup"><span data-stu-id="65f7f-105">It creates a simple sample HR database and use it for importing some users and their group membership.</span></span>

## <a name="prepare-the-sample-database"></a><span data-ttu-id="65f7f-106">準備範例資料庫</span><span class="sxs-lookup"><span data-stu-id="65f7f-106">Prepare the sample database</span></span>
<span data-ttu-id="65f7f-107">在執行 SQL Server 的伺服器上，執行可在[附錄 A](#appendix-a) 中找到的 SQL 指令碼。這會建立名為 GSQLDEMO 的範例資料庫。</span><span class="sxs-lookup"><span data-stu-id="65f7f-107">On a server running SQL Server, run the SQL script found in [Appendix A](#appendix-a). This script creates a sample database with the name GSQLDEMO.</span></span> <span data-ttu-id="65f7f-108">適用於所建立資料庫的物件模型如下圖所示︰</span><span class="sxs-lookup"><span data-stu-id="65f7f-108">The object model for the created database looks like this picture:</span></span>  
<span data-ttu-id="65f7f-109">![物件模型](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span><span class="sxs-lookup"><span data-stu-id="65f7f-109">![Object Model](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span></span>

<span data-ttu-id="65f7f-110">您也可以建立想要用來連接到資料庫的使用者。</span><span class="sxs-lookup"><span data-stu-id="65f7f-110">Also create a user you want to use to connect to the database.</span></span> <span data-ttu-id="65f7f-111">在本逐步解說中，使用者將稱為 FABRIKAM\SQLUser 且位於網域中。</span><span class="sxs-lookup"><span data-stu-id="65f7f-111">In this walkthrough, the user is called FABRIKAM\SQLUser and located in the domain.</span></span>

## <a name="create-the-odbc-connection-file"></a><span data-ttu-id="65f7f-112">建立 ODBC 連接檔案</span><span class="sxs-lookup"><span data-stu-id="65f7f-112">Create the ODBC connection file</span></span>
<span data-ttu-id="65f7f-113">一般 SQL 連接器會使用 ODBC 連接到遠端伺服器。</span><span class="sxs-lookup"><span data-stu-id="65f7f-113">The Generic SQL Connector is using ODBC to connect to the remote server.</span></span> <span data-ttu-id="65f7f-114">首先我們需要建立含有 ODBC 連接資訊的檔案。</span><span class="sxs-lookup"><span data-stu-id="65f7f-114">First we need to create a file with the ODBC connection information.</span></span>

1. <span data-ttu-id="65f7f-115">在伺服器上啟動 ODBC 管理公用程式︰</span><span class="sxs-lookup"><span data-stu-id="65f7f-115">Start the ODBC management utility on your server:</span></span>  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. <span data-ttu-id="65f7f-117">選取 [檔案 DSN] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="65f7f-117">Select the tab **File DSN**.</span></span> <span data-ttu-id="65f7f-118">按一下 [新增...] 。</span><span class="sxs-lookup"><span data-stu-id="65f7f-118">Click **Add...**.</span></span>  
   <span data-ttu-id="65f7f-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span><span class="sxs-lookup"><span data-stu-id="65f7f-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span></span>
3. <span data-ttu-id="65f7f-120">最新的驅動程式可正常運作，因此請選取它，然後按 [下一步 >]。</span><span class="sxs-lookup"><span data-stu-id="65f7f-120">The out-of-box driver works fine, so select it and click **Next>**.</span></span>  
   <span data-ttu-id="65f7f-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span><span class="sxs-lookup"><span data-stu-id="65f7f-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span></span>
4. <span data-ttu-id="65f7f-122">為檔案名稱，例如 **GenericSQL**。</span><span class="sxs-lookup"><span data-stu-id="65f7f-122">Give the file a name, such as **GenericSQL**.</span></span>  
   <span data-ttu-id="65f7f-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span><span class="sxs-lookup"><span data-stu-id="65f7f-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span></span>
5. <span data-ttu-id="65f7f-124">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="65f7f-124">Click **Finish**.</span></span>  
   <span data-ttu-id="65f7f-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span><span class="sxs-lookup"><span data-stu-id="65f7f-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span></span>
6. <span data-ttu-id="65f7f-126">設定連接的時機</span><span class="sxs-lookup"><span data-stu-id="65f7f-126">Time to configure the connection.</span></span> <span data-ttu-id="65f7f-127">為資料來源提供良好的說明，並提供執行 SQL Server 的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="65f7f-127">Give the data source a good description and provide the name of the server running SQL Server.</span></span>  
   ![ODBC5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. <span data-ttu-id="65f7f-129">選取如何使用 SQL 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="65f7f-129">Select how to authenticate with SQL.</span></span> <span data-ttu-id="65f7f-130">在此案例中，我們會使用 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="65f7f-130">In this case, we use Windows Authentication.</span></span>  
   ![ODBC6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. <span data-ttu-id="65f7f-132">提供範例資料庫的名稱 **GSQLDEMO**。</span><span class="sxs-lookup"><span data-stu-id="65f7f-132">Provide the name of the sample database, **GSQLDEMO**.</span></span>  
   <span data-ttu-id="65f7f-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span><span class="sxs-lookup"><span data-stu-id="65f7f-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span></span>
9. <span data-ttu-id="65f7f-134">將此畫面上的所有項目保留為預設值。</span><span class="sxs-lookup"><span data-stu-id="65f7f-134">Keep everything default on this screen.</span></span> <span data-ttu-id="65f7f-135">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="65f7f-135">Click **Finish**.</span></span>  
   <span data-ttu-id="65f7f-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span><span class="sxs-lookup"><span data-stu-id="65f7f-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span></span>
10. <span data-ttu-id="65f7f-137">若要確認一切會如預期般運作，請按一下 [測試資料來源] 。</span><span class="sxs-lookup"><span data-stu-id="65f7f-137">To verify everything is working as expected, click **Test Data Source**.</span></span>  
    <span data-ttu-id="65f7f-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span><span class="sxs-lookup"><span data-stu-id="65f7f-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span></span>
11. <span data-ttu-id="65f7f-139">確定測試成功。</span><span class="sxs-lookup"><span data-stu-id="65f7f-139">Make sure the test is successful.</span></span>  
    ![ODBC10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. <span data-ttu-id="65f7f-141">ODBC 組態檔現在應該會顯示於 [檔案 DSN] 中。</span><span class="sxs-lookup"><span data-stu-id="65f7f-141">The ODBC configuration file should now be visible in File DSN.</span></span>  
    ![ODBC11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

<span data-ttu-id="65f7f-143">我們現在已經擁有所需的檔案，就能開始建立連接器。</span><span class="sxs-lookup"><span data-stu-id="65f7f-143">We now have the file we need and can start creating the Connector.</span></span>

## <a name="create-the-generic-sql-connector"></a><span data-ttu-id="65f7f-144">建立一般 SQL 連接器</span><span class="sxs-lookup"><span data-stu-id="65f7f-144">Create the Generic SQL Connector</span></span>
1. <span data-ttu-id="65f7f-145">在 Synchronization Service Manager UI 中，選取 [連接器] 和 [建立]。</span><span class="sxs-lookup"><span data-stu-id="65f7f-145">In the Synchronization Service Manager UI, select **Connectors** and **Create**.</span></span> <span data-ttu-id="65f7f-146">選取 [一般 SQL (Microsoft)]  並為它提供描述性名稱。</span><span class="sxs-lookup"><span data-stu-id="65f7f-146">Select **Generic SQL (Microsoft)** and give it a descriptive name.</span></span>  
   <span data-ttu-id="65f7f-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span><span class="sxs-lookup"><span data-stu-id="65f7f-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span></span>
2. <span data-ttu-id="65f7f-148">尋找您在上一節中建立的 DSN 檔案，然後將它上傳到伺服器。</span><span class="sxs-lookup"><span data-stu-id="65f7f-148">Find the DSN file you created in the previous section and upload it to the server.</span></span> <span data-ttu-id="65f7f-149">提供認證以連接到資料庫。</span><span class="sxs-lookup"><span data-stu-id="65f7f-149">Provide the credentials to connect to the database.</span></span>  
   ![Connector2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. <span data-ttu-id="65f7f-151">在本逐步解說中，為方便起見，我們假設有兩個物件類型：**User** 和 **Group**。</span><span class="sxs-lookup"><span data-stu-id="65f7f-151">In this walkthrough, we are making it easy for us and say that there are two object types, **User** and **Group**.</span></span>
   <span data-ttu-id="65f7f-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span><span class="sxs-lookup"><span data-stu-id="65f7f-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span></span>
4. <span data-ttu-id="65f7f-153">為了尋找屬性，我們想要讓連接器自行查看資料表，藉以偵測這些屬性。</span><span class="sxs-lookup"><span data-stu-id="65f7f-153">To find the attributes, we want the Connector to detect those attributes by looking at the table itself.</span></span> <span data-ttu-id="65f7f-154">由於 **Users** 是 SQL 中的保留字，因此提供時需要加上方括號 [ ]。</span><span class="sxs-lookup"><span data-stu-id="65f7f-154">Since **Users** is a reserved word in SQL, we need to provide it in square brackets [ ].</span></span>  
   <span data-ttu-id="65f7f-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span><span class="sxs-lookup"><span data-stu-id="65f7f-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span></span>
5. <span data-ttu-id="65f7f-156">定義錨點屬性和 DN 屬性的時機。</span><span class="sxs-lookup"><span data-stu-id="65f7f-156">Time to define the anchor attribute and the DN attribute.</span></span> <span data-ttu-id="65f7f-157">我們針對 **Users**使用兩個屬性 (username 和 EmployeeID) 的組合。</span><span class="sxs-lookup"><span data-stu-id="65f7f-157">For **Users**, we use the combination of the two attributes username and EmployeeID.</span></span> <span data-ttu-id="65f7f-158">我們針對 **group**使用GroupName (在真實生活中並不實際，但對本逐步解說而言，它是可行的)。</span><span class="sxs-lookup"><span data-stu-id="65f7f-158">For **group**, we use GroupName (not realistic in real-life, but for this walkthrough it works).</span></span>
   <span data-ttu-id="65f7f-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span><span class="sxs-lookup"><span data-stu-id="65f7f-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span></span>
6. <span data-ttu-id="65f7f-160">並非所有屬性類型都可以在 SQL 資料庫中偵測到。</span><span class="sxs-lookup"><span data-stu-id="65f7f-160">Not all attribute types can be detected in a SQL database.</span></span> <span data-ttu-id="65f7f-161">特別是無法偵測到參考屬性類型。</span><span class="sxs-lookup"><span data-stu-id="65f7f-161">The reference attribute type in particular cannot.</span></span> <span data-ttu-id="65f7f-162">針對群組物件類型，我們必須變更 OwnerID 和 MemberID 以供參考。</span><span class="sxs-lookup"><span data-stu-id="65f7f-162">For the group object type, we need to change the OwnerID and MemberID to reference.</span></span>  
   ![Connector6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. <span data-ttu-id="65f7f-164">我們在上一個步驟中選取來做為參考屬性的屬性，要求的物件類型是這些值所參考的物件類型。</span><span class="sxs-lookup"><span data-stu-id="65f7f-164">The attributes we selected as reference attributes in the previous step require the object type these values are a reference to.</span></span> <span data-ttu-id="65f7f-165">在此案例中為 User 物件類型。</span><span class="sxs-lookup"><span data-stu-id="65f7f-165">In our case, the User object type.</span></span>  
   ![Connector7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. <span data-ttu-id="65f7f-167">在 [全域參數] 頁面中，選取 [浮水印] 做為差異策略。</span><span class="sxs-lookup"><span data-stu-id="65f7f-167">On the Global Parameters page, select **Watermark** as the delta strategy.</span></span> <span data-ttu-id="65f7f-168">此外，使用日期/時間格式 **yyyy-MM-dd HH:mm:ss**來輸入。</span><span class="sxs-lookup"><span data-stu-id="65f7f-168">Also type in the date/time format **yyyy-MM-dd HH:mm:ss**.</span></span>
   <span data-ttu-id="65f7f-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span><span class="sxs-lookup"><span data-stu-id="65f7f-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span></span>
9. <span data-ttu-id="65f7f-170">在 [設定資料分割和階層]  頁面上，同時選取這兩種物件類型。</span><span class="sxs-lookup"><span data-stu-id="65f7f-170">On the **Configure Partitions and Hierarchies** page, select both object types.</span></span>
   <span data-ttu-id="65f7f-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span><span class="sxs-lookup"><span data-stu-id="65f7f-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span></span>
10. <span data-ttu-id="65f7f-172">在 [選取物件類型] 和 [選取屬性] 中，選取物件類型和所有屬性。</span><span class="sxs-lookup"><span data-stu-id="65f7f-172">On the **Select Object Types** and **Select Attributes**, select both object types and all attributes.</span></span> <span data-ttu-id="65f7f-173">在 [設定錨點] 頁面上，按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="65f7f-173">On the **Configure Anchors** page, click **Finish**.</span></span>

## <a name="create-run-profiles"></a><span data-ttu-id="65f7f-174">建立執行設定檔</span><span class="sxs-lookup"><span data-stu-id="65f7f-174">Create Run Profiles</span></span>
1. <span data-ttu-id="65f7f-175">在 Synchronization Service Manager UI 中，選取 [連接器] 和 [設定執行設定檔]。</span><span class="sxs-lookup"><span data-stu-id="65f7f-175">In the Synchronization Service Manager UI, select **Connectors**, and **Configure Run Profiles**.</span></span> <span data-ttu-id="65f7f-176">按一下 [新增設定檔]。</span><span class="sxs-lookup"><span data-stu-id="65f7f-176">Click **New Profile**.</span></span> <span data-ttu-id="65f7f-177">我們會從**完整匯入**開始。</span><span class="sxs-lookup"><span data-stu-id="65f7f-177">We start with **Full Import**.</span></span>  
   <span data-ttu-id="65f7f-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span><span class="sxs-lookup"><span data-stu-id="65f7f-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span></span>
2. <span data-ttu-id="65f7f-179">選取類型 [完整匯入 (僅限階段)] 。</span><span class="sxs-lookup"><span data-stu-id="65f7f-179">Select the type **Full Import (Stage Only)**.</span></span>  
   <span data-ttu-id="65f7f-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span><span class="sxs-lookup"><span data-stu-id="65f7f-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span></span>
3. <span data-ttu-id="65f7f-181">選取分割區 **OBJECT=User**。</span><span class="sxs-lookup"><span data-stu-id="65f7f-181">Select the partition **OBJECT=User**.</span></span>  
   <span data-ttu-id="65f7f-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span><span class="sxs-lookup"><span data-stu-id="65f7f-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span></span>
4. <span data-ttu-id="65f7f-183">選取 [資料表] 並輸入 [USERS]。</span><span class="sxs-lookup"><span data-stu-id="65f7f-183">Select **Table** and type **[USERS]**.</span></span> <span data-ttu-id="65f7f-184">向下捲動到多重值物件類型區段，並輸入如下圖所示的資料。</span><span class="sxs-lookup"><span data-stu-id="65f7f-184">Scroll down to the multi-valued object type section and enter the data as in the following picture.</span></span> <span data-ttu-id="65f7f-185">選取 [完成]  以儲存步驟。</span><span class="sxs-lookup"><span data-stu-id="65f7f-185">Select **Finish** to save the step.</span></span>  
   <span data-ttu-id="65f7f-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span><span class="sxs-lookup"><span data-stu-id="65f7f-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span></span>  
   <span data-ttu-id="65f7f-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span><span class="sxs-lookup"><span data-stu-id="65f7f-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span></span>  
5. <span data-ttu-id="65f7f-188">選取 [新增步驟] 。</span><span class="sxs-lookup"><span data-stu-id="65f7f-188">Select **New Step**.</span></span> <span data-ttu-id="65f7f-189">這次選取 [OBJECT=Group] 。</span><span class="sxs-lookup"><span data-stu-id="65f7f-189">This time, select **OBJECT=Group**.</span></span> <span data-ttu-id="65f7f-190">在最後一個頁面上，使用如下圖所示的組態。</span><span class="sxs-lookup"><span data-stu-id="65f7f-190">On the last page, use the configuration as in the following picture.</span></span> <span data-ttu-id="65f7f-191">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="65f7f-191">Click **Finish**.</span></span>  
   <span data-ttu-id="65f7f-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span><span class="sxs-lookup"><span data-stu-id="65f7f-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span></span>  
   <span data-ttu-id="65f7f-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span><span class="sxs-lookup"><span data-stu-id="65f7f-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span></span>  
6. <span data-ttu-id="65f7f-194">選用︰如果您想要，您可以設定其他的執行設定檔。</span><span class="sxs-lookup"><span data-stu-id="65f7f-194">Optional: If you want to, you can configure additional run profiles.</span></span> <span data-ttu-id="65f7f-195">在這個逐步解說中，只會使用完整匯入。</span><span class="sxs-lookup"><span data-stu-id="65f7f-195">For this walkthrough, only the Full Import is used.</span></span>
7. <span data-ttu-id="65f7f-196">按一下 [確定]  以完成變更執行設定檔。</span><span class="sxs-lookup"><span data-stu-id="65f7f-196">Click **OK** to finish changing run profiles.</span></span>

## <a name="add-some-test-data-and-test-the-import"></a><span data-ttu-id="65f7f-197">新增一些測試資料並測試匯入</span><span class="sxs-lookup"><span data-stu-id="65f7f-197">Add some test data and test the import</span></span>
<span data-ttu-id="65f7f-198">在範例資料庫中填入部分測試資料。</span><span class="sxs-lookup"><span data-stu-id="65f7f-198">Fill out some test data in your sample database.</span></span> <span data-ttu-id="65f7f-199">當您準備好時，選取 [執行] 和 [完整匯入]。</span><span class="sxs-lookup"><span data-stu-id="65f7f-199">When you are ready, select **Run** and **Full import**.</span></span>

<span data-ttu-id="65f7f-200">以下是具有兩個電話號碼的使用者以及含有一些成員的群組。</span><span class="sxs-lookup"><span data-stu-id="65f7f-200">Here is a user with two phone numbers and a group with some members.</span></span>  
![cs1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![cs2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a><span data-ttu-id="65f7f-203">附錄 A</span><span class="sxs-lookup"><span data-stu-id="65f7f-203">Appendix A</span></span>
<span data-ttu-id="65f7f-204">**建立範例資料庫的 SQL 指令碼**</span><span class="sxs-lookup"><span data-stu-id="65f7f-204">**SQL script to create the sample database**</span></span>

```SQL
---Creating the Database---------
Create Database GSQLDEMO
Go
-------Using the Database-----------
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
