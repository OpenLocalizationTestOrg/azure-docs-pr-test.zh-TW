---
title: "aaaPython 酒瓶 web 應用程式的教學課程 Azure Cosmos DB |Microsoft 文件"
description: "檢閱使用裝載於 Azure 的 Python 酒瓶 web 應用程式的 Azure Cosmos DB toostore 和存取資料的資料庫教學課程。 尋找應用程式開發解決方案。"
keywords: "應用程式部署、python flask、python Web 應用程式、python Web 開發"
services: cosmos-db
documentationcenter: python
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 20ebec18-67c2-4988-a760-be7c30cfb745
ms.service: cosmos-db
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/09/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 87b73c656ed96a7efbd162843a1529d435f027f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a><span data-ttu-id="92992-105">使用 Azure Cosmos DB 建置 Python Flask Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="92992-105">Build a Python Flask web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="92992-106">.NET</span><span class="sxs-lookup"><span data-stu-id="92992-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="92992-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="92992-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="92992-108">Java</span><span class="sxs-lookup"><span data-stu-id="92992-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="92992-109">Python</span><span class="sxs-lookup"><span data-stu-id="92992-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="92992-110">本教學課程會示範如何 toouse Azure Cosmos DB toostore 及存取資料來自 Python web 應用程式裝載於 Azure，並假設您有一些使用經驗，使用 Python 和 Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="92992-110">This tutorial shows you how toouse Azure Cosmos DB toostore and access data from a Python web application hosted on Azure and presumes that you have some prior experience using Python and Azure websites.</span></span>

<span data-ttu-id="92992-111">此資料庫教學課程涵蓋：</span><span class="sxs-lookup"><span data-stu-id="92992-111">This database tutorial covers:</span></span>

1. <span data-ttu-id="92992-112">建立和佈建 Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="92992-112">Creating and provisioning a Cosmos DB account.</span></span>
2. <span data-ttu-id="92992-113">建立 Python Flask 應用程式。</span><span class="sxs-lookup"><span data-stu-id="92992-113">Creating a Python Flask application.</span></span>
3. <span data-ttu-id="92992-114">連接 web 應用程式使用 Cosmos DB tooand。</span><span class="sxs-lookup"><span data-stu-id="92992-114">Connecting tooand using Cosmos DB from your web application.</span></span>
4. <span data-ttu-id="92992-115">部署的 hello web 應用程式 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="92992-115">Deploying hello web application tooAzure.</span></span>

<span data-ttu-id="92992-116">遵循此教學課程中，您將建立簡單的投票應用程式，可讓您輪詢的 toovote。</span><span class="sxs-lookup"><span data-stu-id="92992-116">By following this tutorial, you will build a simple voting application that allows you toovote for a poll.</span></span>

![建立此資料庫教學課程中的 hello 投票應用程式的螢幕擷取畫面](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a><span data-ttu-id="92992-118">資料庫教學課程必要條件</span><span class="sxs-lookup"><span data-stu-id="92992-118">Database tutorial prerequisites</span></span>
<span data-ttu-id="92992-119">這篇文章中的 hello 指示之前，您應該確定您擁有 hello 安裝下列項目：</span><span class="sxs-lookup"><span data-stu-id="92992-119">Before following hello instructions in this article, you should ensure that you have hello following installed:</span></span>

* <span data-ttu-id="92992-120">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="92992-120">An active Azure account.</span></span> <span data-ttu-id="92992-121">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="92992-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="92992-122">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="92992-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
 
    <span data-ttu-id="92992-123">或</span><span class="sxs-lookup"><span data-stu-id="92992-123">OR</span></span> 

    <span data-ttu-id="92992-124">Hello 的本機安裝[Azure Cosmos DB 模擬器](local-emulator.md)。</span><span class="sxs-lookup"><span data-stu-id="92992-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="92992-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/)。</span><span class="sxs-lookup"><span data-stu-id="92992-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="92992-126">[Python Tools for Visual Studio](https://github.com/Microsoft/PTVS/)。</span><span class="sxs-lookup"><span data-stu-id="92992-126">[Python Tools for Visual Studio](https://github.com/Microsoft/PTVS/).</span></span>  
* <span data-ttu-id="92992-127">[Microsoft Azure SDK for Python 2.7](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="92992-127">[Microsoft Azure SDK for Python 2.7](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="92992-128">[Python 2.7.13](https://www.python.org/downloads/windows/)。</span><span class="sxs-lookup"><span data-stu-id="92992-128">[Python 2.7.13](https://www.python.org/downloads/windows/).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="92992-129">如果您要安裝 Python 2.7 hello 第一次，請確定在 hello 自訂 Python 2.7.13 畫面中，您選取**新增 python.exe tooPath**。</span><span class="sxs-lookup"><span data-stu-id="92992-129">If you are installing Python 2.7 for hello first time, ensure that in hello Customize Python 2.7.13 screen, you select **Add python.exe tooPath**.</span></span>
> 
> ![Hello 自訂 Python 2.7.11 畫面上，您需要 tooselect 新增 python.exe tooPath 的螢幕擷取畫面](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* <span data-ttu-id="92992-131">[適用於 Python 2.7 的 Microsoft Visual C++ 編譯器](https://www.microsoft.com/en-us/download/details.aspx?id=44266)。</span><span class="sxs-lookup"><span data-stu-id="92992-131">[Microsoft Visual C++ Compiler for Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="92992-132">步驟 1：建立 Azure Cosmos DB 資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="92992-132">Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="92992-133">我們將從建立 Cosmos DB 帳戶開始著手。</span><span class="sxs-lookup"><span data-stu-id="92992-133">Let's start by creating an Cosmos DB account.</span></span> <span data-ttu-id="92992-134">如果您已經有帳戶，或如果您使用 hello Azure Cosmos DB 模擬器本教學課程中，您可以跳過[步驟 2： 建立新的 Python 酒瓶 web 應用程式](#step-2-create-a-new-python-flask-web-application)。</span><span class="sxs-lookup"><span data-stu-id="92992-134">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create a new Python Flask web application](#step-2-create-a-new-python-flask-web-application).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
<span data-ttu-id="92992-135">我們現在將逐步引導 toocreate 新的 Python 酒瓶 web 應用程式，從 hello 地面的方式。</span><span class="sxs-lookup"><span data-stu-id="92992-135">We will now walk through how toocreate a new Python Flask web application from hello ground up.</span></span>

## <a name="step-2-create-a-new-python-flask-web-application"></a><span data-ttu-id="92992-136">步驟 2：建立新的 Python Flask Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="92992-136">Step 2: Create a new Python Flask web application</span></span>
1. <span data-ttu-id="92992-137">在 Visual Studio 中的 hello**檔案**功能表上，點太**新增**，然後按一下**專案**。</span><span class="sxs-lookup"><span data-stu-id="92992-137">In Visual Studio, on hello **File** menu, point too**New**, and then click **Project**.</span></span>
   
    <span data-ttu-id="92992-138">hello**新專案** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="92992-138">hello **New Project** dialog box appears.</span></span>
2. <span data-ttu-id="92992-139">Hello 左窗格中，展開 **範本**然後**Python**，然後按一下 **Web**。</span><span class="sxs-lookup"><span data-stu-id="92992-139">In hello left pane, expand **Templates** and then **Python**, and then click **Web**.</span></span> 
3. <span data-ttu-id="92992-140">選取**酒瓶 Web 專案**hello 中央窗格中，然後在 hello**名稱**方塊中，輸入**教學課程**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="92992-140">Select **Flask  Web Project** in hello center pane, then in hello **Name** box type **tutorial**, and then click **OK**.</span></span> <span data-ttu-id="92992-141">請記住，hello 中所述，Python 封裝名稱應該是全部小寫， [Python 程式碼的樣式指南](https://www.python.org/dev/peps/pep-0008/#package-and-module-names)。</span><span class="sxs-lookup"><span data-stu-id="92992-141">Remember that Python package names should be all lowercase, as described in hello [Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span></span>
   
    <span data-ttu-id="92992-142">這些新 tooPython 酒瓶，對於 web 應用程式開發架構，可協助您以 Python web 應用程式的建立更為快速。</span><span class="sxs-lookup"><span data-stu-id="92992-142">For those new tooPython Flask, it is a web application development framework that helps you build web applications in Python faster.</span></span>
   
    ![在 Visual Studio 中使用 Python 上左、 Python 酒瓶 Web 專案 hello 名稱方塊中選取 hello 中間和 hello 名稱教學課程中的 hello 反白顯示 hello [新增專案] 視窗的螢幕擷取畫面](./media/documentdb-python-application/image9.png)
4. <span data-ttu-id="92992-144">在 hello **Python Tools for Visual Studio**視窗中，按一下 **安裝在虛擬環境**。</span><span class="sxs-lookup"><span data-stu-id="92992-144">In hello **Python Tools for Visual Studio** window, click **Install into a virtual environment**.</span></span> 
   
    ![Hello database 教學課程-Python Tools for Visual Studio 視窗的螢幕擷取畫面](./media/documentdb-python-application/python-install-virtual-environment.png)
5. <span data-ttu-id="92992-146">在 hello**加入虛擬環境**視窗中，您可以接受 hello 預設值，並使用 Python 2.7 hello 基底的環境，因為 PyDocumentDB 目前不支援 Python 3.x 中，然後再按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="92992-146">In hello **Add Virtual Environment** window, you can accept hello defaults and use Python 2.7 as hello base environment because PyDocumentDB does not currently support Python 3.x, and then click **Create**.</span></span> <span data-ttu-id="92992-147">這會設定為您的專案所需的 hello Python 虛擬環境。</span><span class="sxs-lookup"><span data-stu-id="92992-147">This sets up hello required Python virtual environment for your project.</span></span>
   
    ![Hello database 教學課程-Python Tools for Visual Studio 視窗的螢幕擷取畫面](./media/documentdb-python-application/image10_A.png)
   
    <span data-ttu-id="92992-149">hello 輸出 視窗會顯示`Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.`hello 環境已成功安裝。</span><span class="sxs-lookup"><span data-stu-id="92992-149">hello output window displays `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` when hello environment is successfully installed.</span></span>

## <a name="step-3-modify-hello-python-flask-web-application"></a><span data-ttu-id="92992-150">步驟 3： 修改 hello Python 酒瓶 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="92992-150">Step 3: Modify hello Python Flask web application</span></span>
### <a name="add-hello-python-flask-packages-tooyour-project"></a><span data-ttu-id="92992-151">加入 hello Python 酒瓶封裝 tooyour 專案</span><span class="sxs-lookup"><span data-stu-id="92992-151">Add hello Python Flask packages tooyour project</span></span>
<span data-ttu-id="92992-152">您的專案設定後，您需要 tooadd 所需的 hello 酒瓶封裝 tooyour 專案，包括 pydocumentdb，DocumentDB 的 hello Python 封裝。</span><span class="sxs-lookup"><span data-stu-id="92992-152">After your project is set up, you'll need tooadd hello required Flask packages tooyour project, including pydocumentdb, hello Python package for DocumentDB.</span></span>

1. <span data-ttu-id="92992-153">在 [方案總管] 中，開啟名為 hello 檔案**requirements.txt**並取代 hello 下列中的 hello 內容：</span><span class="sxs-lookup"><span data-stu-id="92992-153">In Solution Explorer, open hello file named **requirements.txt** and replace hello contents with hello following:</span></span>
   
        flask==0.9
        flask-mail==0.7.6
        sqlalchemy==0.7.9
        flask-sqlalchemy==0.16
        sqlalchemy-migrate==0.7.2
        flask-whooshalchemy==0.55a
        flask-wtf==0.8.4
        pytz==2013b
        flask-babel==0.8
        flup
        pydocumentdb>=1.0.0
2. <span data-ttu-id="92992-154">儲存 hello **requirements.txt**檔案。</span><span class="sxs-lookup"><span data-stu-id="92992-154">Save hello **requirements.txt** file.</span></span> 
3. <span data-ttu-id="92992-155">在「方案總管」中以滑鼠右鍵按一下 [env]，然後按一下 [從 requirements.txt 安裝]。</span><span class="sxs-lookup"><span data-stu-id="92992-155">In Solution Explorer, right-click **env** and click **Install from requirements.txt**.</span></span>
   
    ![螢幕擷取畫面顯示 env (Python 2.7) 從 requirements.txt hello 清單中反白顯示所選取的安裝](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    <span data-ttu-id="92992-157">安裝成功後，hello [輸出] 視窗會顯示 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="92992-157">After successful installation, hello output window displays hello following:</span></span>
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > <span data-ttu-id="92992-158">在罕見的情況下，您可能會看到 hello [輸出] 視窗中的失敗。</span><span class="sxs-lookup"><span data-stu-id="92992-158">In rare cases, you might see a failure in hello output window.</span></span> <span data-ttu-id="92992-159">如果發生這種情況，請檢查 hello 錯誤是否相關的 toocleanup。</span><span class="sxs-lookup"><span data-stu-id="92992-159">If this happens, check if hello error is related toocleanup.</span></span> <span data-ttu-id="92992-160">有時 hello 清除會失敗，但是 hello 安裝仍然會成功 （向上捲動 hello 輸出視窗 tooverify 這）。</span><span class="sxs-lookup"><span data-stu-id="92992-160">Sometimes hello cleanup fails, but hello installation will still be successful (scroll up in hello output window tooverify this).</span></span> <span data-ttu-id="92992-161">您可以檢查您安裝[確認 hello 虛擬環境](#verify-the-virtual-environment)。</span><span class="sxs-lookup"><span data-stu-id="92992-161">You can check your installation by [Verifying hello virtual environment](#verify-the-virtual-environment).</span></span> <span data-ttu-id="92992-162">如果 hello 安裝失敗，但 hello 驗證會成功，則確定 toocontinue。</span><span class="sxs-lookup"><span data-stu-id="92992-162">If hello installation failed but hello verification is successful, it's OK toocontinue.</span></span>
   > 
   > 

### <a name="verify-hello-virtual-environment"></a><span data-ttu-id="92992-163">確認 hello 虛擬環境</span><span class="sxs-lookup"><span data-stu-id="92992-163">Verify hello virtual environment</span></span>
<span data-ttu-id="92992-164">讓我們來確定一切都安裝正確。</span><span class="sxs-lookup"><span data-stu-id="92992-164">Let's make sure that everything is installed correctly.</span></span>

1. <span data-ttu-id="92992-165">按建置 hello 方案**Ctrl**+**Shift**+**B**。</span><span class="sxs-lookup"><span data-stu-id="92992-165">Build hello solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="92992-166">Hello 建置成功後，請按下啟動 hello 網站**F5**。</span><span class="sxs-lookup"><span data-stu-id="92992-166">Once hello build succeeds, start hello website by pressing **F5**.</span></span> <span data-ttu-id="92992-167">這會啟動 hello 酒瓶程式開發伺服器，並啟動 web 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="92992-167">This launches hello Flask development server and starts your web browser.</span></span> <span data-ttu-id="92992-168">您應該會看到下列頁面的 hello。</span><span class="sxs-lookup"><span data-stu-id="92992-168">You should see hello following page.</span></span>
   
    ![hello 空 Python 酒瓶的 web 開發專案在瀏覽器](./media/documentdb-python-application/image12.png)
3. <span data-ttu-id="92992-170">停止偵錯 hello 網站按**Shift**+**F5** Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="92992-170">Stop debugging hello website by pressing **Shift**+**F5** in Visual Studio.</span></span>

### <a name="create-database-collection-and-document-definitions"></a><span data-ttu-id="92992-171">建立資料庫、集合和文件定義</span><span class="sxs-lookup"><span data-stu-id="92992-171">Create database, collection, and document definitions</span></span>
<span data-ttu-id="92992-172">現在請加入新檔案並更新其他檔案，以建立您的投票應用程式。</span><span class="sxs-lookup"><span data-stu-id="92992-172">Now let's create your voting application by adding new files and updating others.</span></span>

1. <span data-ttu-id="92992-173">在 方案總管 中，以滑鼠右鍵按一下 hello**教學課程**專案中，按一下 **新增**，然後按一下**新項目**。</span><span class="sxs-lookup"><span data-stu-id="92992-173">In Solution Explorer, right-click hello **tutorial** project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="92992-174">選取**空的 Python 檔案**和名稱 hello 檔案**forms.py**。</span><span class="sxs-lookup"><span data-stu-id="92992-174">Select **Empty Python File** and name hello file **forms.py**.</span></span>  
2. <span data-ttu-id="92992-175">新增下列程式碼 toohello forms.py 檔案中的 hello，然後將檔案儲存 hello。</span><span class="sxs-lookup"><span data-stu-id="92992-175">Add hello following code toohello forms.py file, and then save hello file.</span></span>

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-hello-required-imports-tooviewspy"></a><span data-ttu-id="92992-176">加入所需的 hello 匯入 tooviews.py</span><span class="sxs-lookup"><span data-stu-id="92992-176">Add hello required imports tooviews.py</span></span>
1. <span data-ttu-id="92992-177">在 方案總管 中，展開 hello**教學課程**資料夾，然後開啟 hello **views.py**檔案。</span><span class="sxs-lookup"><span data-stu-id="92992-177">In Solution Explorer, expand hello **tutorial** folder, and open hello **views.py** file.</span></span> 
2. <span data-ttu-id="92992-178">新增下列匯入陳述式 toohello hello 頂端的 hello **views.py**檔案，然後儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="92992-178">Add hello following import statements toohello top of hello **views.py** file, then save hello file.</span></span> <span data-ttu-id="92992-179">這些匯入 Cosmos DB PythonSDK 和 hello 酒瓶封裝。</span><span class="sxs-lookup"><span data-stu-id="92992-179">These import Cosmos DB's PythonSDK and hello Flask packages.</span></span>
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a><span data-ttu-id="92992-180">建立資料庫、集合和文件</span><span class="sxs-lookup"><span data-stu-id="92992-180">Create database, collection, and document</span></span>
* <span data-ttu-id="92992-181">仍在**views.py**，加入下列程式碼 toohello 結尾 hello 檔案 hello。</span><span class="sxs-lookup"><span data-stu-id="92992-181">Still in **views.py**, add hello following code toohello end of hello file.</span></span> <span data-ttu-id="92992-182">這會負責建立 hello hello 表單所使用的資料庫。</span><span class="sxs-lookup"><span data-stu-id="92992-182">This takes care of creating hello database used by hello form.</span></span> <span data-ttu-id="92992-183">請勿刪除任何現有的程式碼 hello 中**views.py**。</span><span class="sxs-lookup"><span data-stu-id="92992-183">Do not delete any of hello existing code in **views.py**.</span></span> <span data-ttu-id="92992-184">只是附加此 toohello 結束。</span><span class="sxs-lookup"><span data-stu-id="92992-184">Simply append this toohello end.</span></span>

```python
@app.route('/create')
def create():
    """Renders hello contact page."""
    client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

    # Attempt toodelete hello database.  This allows this toobe used toorecreate as well as create
    try:
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))
        client.DeleteDatabase(db['_self'])
    except:
        pass

    # Create database
    db = client.CreateDatabase({ 'id': config.DOCUMENTDB_DATABASE })

    # Create collection
    collection = client.CreateCollection(db['_self'],{ 'id': config.DOCUMENTDB_COLLECTION })

    # Create document
    document = client.CreateDocument(collection['_self'],
        { 'id': config.DOCUMENTDB_DOCUMENT,
          'Web Site': 0,
          'Cloud Service': 0,
          'Virtual Machine': 0,
          'name': config.DOCUMENTDB_DOCUMENT 
        })

    return render_template(
       'create.html',
        title='Create Page',
        year=datetime.now().year,
        message='You just created a new database, collection, and document.  Your old votes have been deleted')
```


### <a name="read-database-collection-document-and-submit-form"></a><span data-ttu-id="92992-185">讀取資料庫、集合、文件並送出表單</span><span class="sxs-lookup"><span data-stu-id="92992-185">Read database, collection, document, and submit form</span></span>
* <span data-ttu-id="92992-186">仍在**views.py**，加入下列程式碼 toohello 結尾 hello 檔案 hello。</span><span class="sxs-lookup"><span data-stu-id="92992-186">Still in **views.py**, add hello following code toohello end of hello file.</span></span> <span data-ttu-id="92992-187">這會負責設定 hello 形式，讀取 hello 資料庫、 集合和文件。</span><span class="sxs-lookup"><span data-stu-id="92992-187">This takes care of setting up hello form, reading hello database, collection, and document.</span></span> <span data-ttu-id="92992-188">請勿刪除任何現有的程式碼 hello 中**views.py**。</span><span class="sxs-lookup"><span data-stu-id="92992-188">Do not delete any of hello existing code in **views.py**.</span></span> <span data-ttu-id="92992-189">只是附加此 toohello 結束。</span><span class="sxs-lookup"><span data-stu-id="92992-189">Simply append this toohello end.</span></span>

```python
@app.route('/vote', methods=['GET', 'POST'])
def vote(): 
    form = VoteForm()
    replaced_document ={}
    if form.validate_on_submit(): # is user submitted vote  
        client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

        # Read databases and take first since id should not be duplicated.
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))

        # Read collections and take first since id should not be duplicated.
        coll = next((coll for coll in client.ReadCollections(db['_self']) if coll['id'] == config.DOCUMENTDB_COLLECTION))

        # Read documents and take first since id should not be duplicated.
        doc = next((doc for doc in client.ReadDocuments(coll['_self']) if doc['id'] == config.DOCUMENTDB_DOCUMENT))

        # Take hello data from hello deploy_preference and increment our database
        doc[form.deploy_preference.data] = doc[form.deploy_preference.data] + 1
        replaced_document = client.ReplaceDocument(doc['_self'], doc)

        # Create a model toopass tooresults.html
        class VoteObject:
            choices = dict()
            total_votes = 0

        vote_object = VoteObject()
        vote_object.choices = {
            "Web Site" : doc['Web Site'],
            "Cloud Service" : doc['Cloud Service'],
            "Virtual Machine" : doc['Virtual Machine']
        }
        vote_object.total_votes = sum(vote_object.choices.values())

        return render_template(
            'results.html', 
            year=datetime.now().year, 
            vote_object = vote_object)

    else :
        return render_template(
            'vote.html', 
            title = 'Vote',
            year=datetime.now().year,
            form = form)
```


### <a name="create-hello-html-files"></a><span data-ttu-id="92992-190">建立 hello HTML 檔案</span><span class="sxs-lookup"><span data-stu-id="92992-190">Create hello HTML files</span></span>
1. <span data-ttu-id="92992-191">在 方案總管中 hello**教學課程**資料夾中，右邊按一下 hello**範本**資料夾中，按一下 **新增**，然後按一下**新項目**。</span><span class="sxs-lookup"><span data-stu-id="92992-191">In Solution Explorer, in hello **tutorial** folder, right click hello **templates** folder, click **Add**, and then click **New Item**.</span></span> 
2. <span data-ttu-id="92992-192">選取**HTML 網頁**，然後在 [hello] 名稱方塊中鍵入**create.html**。</span><span class="sxs-lookup"><span data-stu-id="92992-192">Select **HTML Page**, and then in hello name box type **create.html**.</span></span> 
3. <span data-ttu-id="92992-193">重複步驟 1 和 2 toocreate 兩個其他的 HTML 檔案： results.html 和 vote.html。</span><span class="sxs-lookup"><span data-stu-id="92992-193">Repeat steps 1 and 2 toocreate two additional HTML files: results.html and vote.html.</span></span>
4. <span data-ttu-id="92992-194">新增下列程式碼太 hello**create.html**在 hello`<body>`項目。</span><span class="sxs-lookup"><span data-stu-id="92992-194">Add hello following code too**create.html** in hello `<body>` element.</span></span> <span data-ttu-id="92992-195">此程式碼可顯示訊息，指出我們已建立新的資料庫、集合和文件。</span><span class="sxs-lookup"><span data-stu-id="92992-195">It displays a message stating that we created a new database, collection, and document.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. <span data-ttu-id="92992-196">新增下列程式碼太 hello**results.html**在 hello `<body`> 項目。</span><span class="sxs-lookup"><span data-stu-id="92992-196">Add hello following code too**results.html** in hello `<body`> element.</span></span> <span data-ttu-id="92992-197">它會顯示 hello 輪詢 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="92992-197">It displays hello results of hello poll.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Results of hello vote</h2>
        <br />
   
    {% for choice in vote_object.choices %}
    <div class="row">
        <div class="col-sm-5">{{choice}}</div>
            <div class="col-sm-5">
                <div class="progress">
                    <div class="progress-bar" role="progressbar" aria-valuenow="{{vote_object.choices[choice]}}" aria-valuemin="0" aria-valuemax="{{vote_object.total_votes}}" style="width: {{(vote_object.choices[choice]/vote_object.total_votes)*100}}%;">
                                {{vote_object.choices[choice]}}
                </div>
            </div>
            </div>
    </div>
    {% endfor %}
   
    <br />
    <a class="btn btn-primary" href="{{ url_for('vote') }}">Vote again?</a>
    {% endblock %}
    ```
6. <span data-ttu-id="92992-198">新增下列程式碼太 hello**vote.html**在 hello `<body`> 項目。</span><span class="sxs-lookup"><span data-stu-id="92992-198">Add hello following code too**vote.html** in hello `<body`> element.</span></span> <span data-ttu-id="92992-199">它會顯示 hello 輪詢，並接受 hello 投票。</span><span class="sxs-lookup"><span data-stu-id="92992-199">It displays hello poll and accepts hello votes.</span></span> <span data-ttu-id="92992-200">在註冊 hello 投票，hello 控制權會傳遞透過 tooviews.py 我們將在此辨識 hello 投票轉換，並據以附加 hello 文件。</span><span class="sxs-lookup"><span data-stu-id="92992-200">On registering hello votes, hello control is passed over tooviews.py where we will recognize hello vote cast and append hello document accordingly.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>What is your favorite way toohost an application on Azure?</h2>
    <form action="" method="post" name="vote">
        {{form.hidden_tag()}}
            {{form.deploy_preference}}
            <button class="btn btn-primary" type="submit">Vote</button>
    </form>
    {% endblock %}
    ```
7. <span data-ttu-id="92992-201">在 hello**範本**資料夾，取代 hello 內容**index.html** hello 下列。</span><span class="sxs-lookup"><span data-stu-id="92992-201">In hello **templates** folder, replace hello contents of **index.html** with hello following.</span></span> <span data-ttu-id="92992-202">這可做為 hello 登陸頁面，您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="92992-202">This serves as hello landing page for your application.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear hello Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-hello-initpy"></a><span data-ttu-id="92992-203">加入組態檔並變更 hello \_ \_init\_\_.py</span><span class="sxs-lookup"><span data-stu-id="92992-203">Add a configuration file and change hello \_\_init\_\_.py</span></span>
1. <span data-ttu-id="92992-204">在 方案總管 中，以滑鼠右鍵按一下 hello**教學課程**專案中，按一下 **新增**，按一下**新項目**，選取**空的 Python 檔案**，然後名稱 hello 檔**config.py**。</span><span class="sxs-lookup"><span data-stu-id="92992-204">In Solution Explorer, right-click hello **tutorial** project, click **Add**, click **New Item**, select **Empty Python File**, and then name hello file **config.py**.</span></span> <span data-ttu-id="92992-205">Flask 中的表單需要使用此組態檔案。</span><span class="sxs-lookup"><span data-stu-id="92992-205">This config file is required by forms in Flask.</span></span> <span data-ttu-id="92992-206">您可以使用 tooprovide 以及祕密金鑰。</span><span class="sxs-lookup"><span data-stu-id="92992-206">You can use it tooprovide a secret key as well.</span></span> <span data-ttu-id="92992-207">但本教學課程不需要用到此金鑰。</span><span class="sxs-lookup"><span data-stu-id="92992-207">This key is not needed for this tutorial though.</span></span>
2. <span data-ttu-id="92992-208">將 hello 面一行加入程式碼 tooconfig.py，您將需要 tooalter hello 值**DOCUMENTDB\_主機**和**DOCUMENTDB\_金鑰**hello 下一個步驟中。</span><span class="sxs-lookup"><span data-stu-id="92992-208">Add hello following code tooconfig.py, you'll need tooalter hello values of **DOCUMENTDB\_HOST** and **DOCUMENTDB\_KEY** in hello next step.</span></span>
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. <span data-ttu-id="92992-209">在 hello [Azure 入口網站](https://portal.azure.com/)，瀏覽 toohello**金鑰**刀鋒視窗中的按一下**瀏覽**， **Azure Cosmos DB 帳戶**，連按兩下 hello 名稱hello 的帳戶 toouse，，然後按一下hello**金鑰**按鈕在 hello **Essentials**區域。</span><span class="sxs-lookup"><span data-stu-id="92992-209">In hello [Azure portal](https://portal.azure.com/), navigate toohello **Keys** blade by clicking **Browse**, **Azure Cosmos DB Accounts**, double-click hello name of hello account toouse, and then click hello **Keys** button in hello **Essentials** area.</span></span> <span data-ttu-id="92992-210">在 hello**金鑰**刀鋒視窗，複製 hello **URI**值並貼到 hello **config.py**檔案，做為 hello 的 hello 值**DOCUMENTDB\_主機**屬性。</span><span class="sxs-lookup"><span data-stu-id="92992-210">In hello **Keys** blade, copy hello **URI** value and paste it into hello **config.py** file, as hello value for hello **DOCUMENTDB\_HOST** property.</span></span> 
4. <span data-ttu-id="92992-211">Hello hello 中的 Azure 入口網站中**金鑰**刀鋒視窗中，複製 hello 值 hello**主索引鍵**或 hello**次要金鑰**，並將它貼到 hello **config.py**檔案，做為 hello 的 hello 值**DOCUMENTDB\_金鑰**屬性。</span><span class="sxs-lookup"><span data-stu-id="92992-211">Back in hello Azure portal, in hello **Keys** blade, copy hello value of hello **Primary Key** or hello **Secondary Key**, and paste it into hello **config.py** file, as hello value for hello **DOCUMENTDB\_KEY** property.</span></span>
5. <span data-ttu-id="92992-212">在 hello  **\_ \_init\_\_.py** file、 add hello 行下。</span><span class="sxs-lookup"><span data-stu-id="92992-212">In hello **\_\_init\_\_.py** file, add hello following line.</span></span> 
   
        app.config.from_object('config')
   
    <span data-ttu-id="92992-213">使 hello hello 檔案內容：</span><span class="sxs-lookup"><span data-stu-id="92992-213">So that hello content of hello file is:</span></span>
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. <span data-ttu-id="92992-214">加入所有 hello 檔案之後, 方案總管 中看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="92992-214">After adding all hello files, Solution Explorer should look like this:</span></span>
   
    ![Hello Visual Studio 方案總管 視窗的螢幕擷取畫面](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a><span data-ttu-id="92992-216">步驟 4：在本機執行您的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="92992-216">Step 4: Run your web application locally</span></span>
1. <span data-ttu-id="92992-217">按建置 hello 方案**Ctrl**+**Shift**+**B**。</span><span class="sxs-lookup"><span data-stu-id="92992-217">Build hello solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="92992-218">Hello 建置成功後，請按下啟動 hello 網站**F5**。</span><span class="sxs-lookup"><span data-stu-id="92992-218">Once hello build succeeds, start hello website by pressing **F5**.</span></span> <span data-ttu-id="92992-219">您應該會看到下列 hello 螢幕上。</span><span class="sxs-lookup"><span data-stu-id="92992-219">You should see hello following on your screen.</span></span>
   
    ![Hello Python + Azure Cosmos DB 投票應用程式在 web 瀏覽器中顯示的螢幕擷取畫面](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. <span data-ttu-id="92992-221">按一下**建立/清除 hello 投票資料庫**toogenerate hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="92992-221">Click **Create/Clear hello Voting Database** toogenerate hello database.</span></span>
   
    ![螢幕擷取畫面的 hello 建立網頁的 hello web 應用程式 – 開發的詳細資訊](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. <span data-ttu-id="92992-223">然後，按一下 [投票]  ，並選取您的選項。</span><span class="sxs-lookup"><span data-stu-id="92992-223">Then, click **Vote** and select your option.</span></span>
   
    ![Hello 投票問題所造成的 web 應用程式的螢幕擷取畫面](./media/documentdb-python-application/cosmos-db-vote.png)
5. <span data-ttu-id="92992-225">為您轉換每個投票，它會遞增 hello 適當的計數器。</span><span class="sxs-lookup"><span data-stu-id="92992-225">For every vote you cast, it increments hello appropriate counter.</span></span>
   
    ![Hello 結果所示的 hello 投票頁面的螢幕擷取畫面](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. <span data-ttu-id="92992-227">停止偵錯 hello 專案藉由按下 Shift + F5。</span><span class="sxs-lookup"><span data-stu-id="92992-227">Stop debugging hello project by pressing Shift+F5.</span></span>

## <a name="step-5-deploy-hello-web-application-tooazure"></a><span data-ttu-id="92992-228">步驟 5： 部署的 hello web 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="92992-228">Step 5: Deploy hello web application tooAzure</span></span>
<span data-ttu-id="92992-229">既然您已針對 Cosmos DB 正常運作的 hello 完整應用程式時，我們 toodeploy 此 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="92992-229">Now that you have hello complete application working correctly against Cosmos DB, we're going toodeploy this tooAzure.</span></span>

1. <span data-ttu-id="92992-230">以滑鼠右鍵按一下方案總管 中的 hello 專案 (請確定您不是仍在本機執行)，選取**發行**。</span><span class="sxs-lookup"><span data-stu-id="92992-230">Right-click hello project in Solution Explorer (make sure you're not still running it locally) and select **Publish**.</span></span>  
   
     ![Hello 教學課程的螢幕擷取畫面中選取方案總管 中，以 hello 反白顯示的 發佈 選項](./media/documentdb-python-application/image20.png)
2. <span data-ttu-id="92992-232">在 hello**發行**對話方塊中，選取**Microsoft Azure App Service**，選取**建立新**，然後按一下**發行**。</span><span class="sxs-lookup"><span data-stu-id="92992-232">In hello **Publish** dialog box, select **Microsoft Azure App Service**, select **Create New**, and then click **Publish**.</span></span>
   
    ![使用 Microsoft Azure App Service 反白顯示 hello 發行 Web 視窗的螢幕擷取畫面](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. <span data-ttu-id="92992-234">在 hello**建立 App Service**對話方塊方塊中，輸入您的 web 應用程式，連同 hello 名稱您**訂用帳戶**，**資源群組**，和**App Service 方案**，然後按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="92992-234">In hello **Create App Service** dialog box, enter hello name for your web app along with your **Subscription**, **Resource Group**, and **App Service Plan**, then click **Create**.</span></span>
   
    ![Microsoft Azure Web 應用程式視窗 [hello] 視窗的螢幕擷取畫面](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. <span data-ttu-id="92992-236">幾秒後，Visual Studio 將完成發佈 App Service 並啟動瀏覽器，您可以在瀏覽器中看到您方便好用的應用程式已在 Azure 中執行！</span><span class="sxs-lookup"><span data-stu-id="92992-236">In a few seconds, Visual Studio will finish publishing your app service and launch a browser where you can see your handiwork running in Azure!</span></span>

    ![Microsoft Azure Web 應用程式視窗 [hello] 視窗的螢幕擷取畫面](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a><span data-ttu-id="92992-238">疑難排解</span><span class="sxs-lookup"><span data-stu-id="92992-238">Troubleshooting</span></span>
<span data-ttu-id="92992-239">如果這是您已在電腦執行 hello 第一個 Python 應用程式，請確定該 hello 下列資料夾 （或 hello 對等的安裝位置） 都包含在 PATH 變數：</span><span class="sxs-lookup"><span data-stu-id="92992-239">If this is hello first Python app you've run on your computer, ensure that hello following folders (or hello equivalent installation locations) are included in your PATH variable:</span></span>

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

<span data-ttu-id="92992-240">如果您收到錯誤訊息上投票，而且您命名為您的專案名稱以外**教學課程**，請確定 **\_ \_init\_\_.py**參考 hello hello 行正確的專案名稱： `import tutorial.view`。</span><span class="sxs-lookup"><span data-stu-id="92992-240">If you receive an error on your vote page, and you named your project something other than **tutorial**, make sure that **\_\_init\_\_.py** references hello correct project name in hello line: `import tutorial.view`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92992-241">後續步驟</span><span class="sxs-lookup"><span data-stu-id="92992-241">Next steps</span></span>
<span data-ttu-id="92992-242">恭喜！</span><span class="sxs-lookup"><span data-stu-id="92992-242">Congratulations!</span></span> <span data-ttu-id="92992-243">您剛完成第一個 Python web 應用程式使用 Cosmos DB 並發佈它 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="92992-243">You have just completed your first Python web application using Cosmos DB and published it tooAzure.</span></span>

<span data-ttu-id="92992-244">我們會根據您的意見反應，經常更新並改善此主題。</span><span class="sxs-lookup"><span data-stu-id="92992-244">We update and improve this topic frequently based on your feedback.</span></span>  <span data-ttu-id="92992-245">一次您已經完成 hello 教學課程中，請使用 hello 投票按鈕 hello 頂端和底端的這個頁面上，而且確定 tooinclude 上您想要的 toosee 進行何種改善您的意見反應。</span><span class="sxs-lookup"><span data-stu-id="92992-245">Once you've completed hello tutorial, please using hello voting buttons at hello top and bottom of this page, and be sure tooinclude your feedback on what improvements you want toosee made.</span></span> <span data-ttu-id="92992-246">如果您希望我們 toocontact 您直接，認為您的電子郵件地址可用 tooinclude 註解中。</span><span class="sxs-lookup"><span data-stu-id="92992-246">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="92992-247">tooadd 額外的功能 tooyour web 應用程式中，檢閱 hello Api 可在 hello [Azure Cosmos DB Python SDK](documentdb-sdk-python.md)。</span><span class="sxs-lookup"><span data-stu-id="92992-247">tooadd additional functionality tooyour web application, review hello APIs available in hello [Azure Cosmos DB Python SDK](documentdb-sdk-python.md).</span></span>

<span data-ttu-id="92992-248">如需有關 Azure 中，Visual Studio 和 Python 的詳細資訊，請參閱 hello [Python 開發人員中心](https://azure.microsoft.com/develop/python/)。</span><span class="sxs-lookup"><span data-stu-id="92992-248">For more information about Azure, Visual Studio, and Python, see hello [Python Developer Center](https://azure.microsoft.com/develop/python/).</span></span> 

<span data-ttu-id="92992-249">如需其他的 Python 酒瓶教學課程，請參閱[hello 酒瓶百萬-教學課程中，部分 i: Hello，World ！](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world)。</span><span class="sxs-lookup"><span data-stu-id="92992-249">For additional Python Flask tutorials, see [hello Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span></span> 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com
