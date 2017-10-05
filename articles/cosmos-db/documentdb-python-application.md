---
title: "Azure Cosmos DB 的 Python Flask Web 應用程式教學課程 | Microsoft Docs"
description: "檢閱資料庫教學課程，了解如何使用 Azure Cosmos DB，來儲存和存取 Azure 上所託管的 Python Flask Web 應用程式資料。 尋找應用程式開發解決方案。"
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
ms.openlocfilehash: ed5284b5a265840c43dbc9890082a7c038d22975
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a><span data-ttu-id="7ddaa-105">使用 Azure Cosmos DB 建置 Python Flask Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7ddaa-105">Build a Python Flask web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7ddaa-106">.NET</span><span class="sxs-lookup"><span data-stu-id="7ddaa-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="7ddaa-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="7ddaa-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="7ddaa-108">Java</span><span class="sxs-lookup"><span data-stu-id="7ddaa-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="7ddaa-109">Python</span><span class="sxs-lookup"><span data-stu-id="7ddaa-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="7ddaa-110">本教學課程說明如何使用 Azure Cosmos DB，來儲存和存取 Azure 上所託管的 Python Web 應用程式資料，並假設您先前已有使用 Python 和 Azure 網站的經驗。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-110">This tutorial shows you how to use Azure Cosmos DB to store and access data from a Python web application hosted on Azure and presumes that you have some prior experience using Python and Azure websites.</span></span>

<span data-ttu-id="7ddaa-111">此資料庫教學課程涵蓋：</span><span class="sxs-lookup"><span data-stu-id="7ddaa-111">This database tutorial covers:</span></span>

1. <span data-ttu-id="7ddaa-112">建立和佈建 Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-112">Creating and provisioning a Cosmos DB account.</span></span>
2. <span data-ttu-id="7ddaa-113">建立 Python Flask 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-113">Creating a Python Flask application.</span></span>
3. <span data-ttu-id="7ddaa-114">從 Web 應用程式連線至 Cosmos DB 並加以使用。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-114">Connecting to and using Cosmos DB from your web application.</span></span>
4. <span data-ttu-id="7ddaa-115">將 Web 應用程式部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-115">Deploying the web application to Azure.</span></span>

<span data-ttu-id="7ddaa-116">按照本教學課程進行後，您將建置可讓您舉行投票活動的簡單投票應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-116">By following this tutorial, you will build a simple voting application that allows you to vote for a poll.</span></span>

![本資料庫教學課程所建立之投票應用程式的螢幕擷取畫面](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a><span data-ttu-id="7ddaa-118">資料庫教學課程必要條件</span><span class="sxs-lookup"><span data-stu-id="7ddaa-118">Database tutorial prerequisites</span></span>
<span data-ttu-id="7ddaa-119">在依照本文中的指示進行之前，您應確定已安裝下列項目：</span><span class="sxs-lookup"><span data-stu-id="7ddaa-119">Before following the instructions in this article, you should ensure that you have the following installed:</span></span>

* <span data-ttu-id="7ddaa-120">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-120">An active Azure account.</span></span> <span data-ttu-id="7ddaa-121">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="7ddaa-122">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
 
    <span data-ttu-id="7ddaa-123">或</span><span class="sxs-lookup"><span data-stu-id="7ddaa-123">OR</span></span> 

    <span data-ttu-id="7ddaa-124">本機安裝的 [Azure Cosmos DB 模擬器](local-emulator.md)。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-124">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="7ddaa-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/)。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="7ddaa-126">[Python Tools for Visual Studio](https://github.com/Microsoft/PTVS/)。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-126">[Python Tools for Visual Studio](https://github.com/Microsoft/PTVS/).</span></span>  
* <span data-ttu-id="7ddaa-127">[Microsoft Azure SDK for Python 2.7](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-127">[Microsoft Azure SDK for Python 2.7](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="7ddaa-128">[Python 2.7.13](https://www.python.org/downloads/windows/)。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-128">[Python 2.7.13](https://www.python.org/downloads/windows/).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="7ddaa-129">如果您是第一次安裝 Python 2.7，請確定在自訂 Python 2.7.13 畫面中，選取 [將 python.exe 加入路徑]。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-129">If you are installing Python 2.7 for the first time, ensure that in the Customize Python 2.7.13 screen, you select **Add python.exe to Path**.</span></span>
> 
> ![自訂 Python 2.7.11 的螢幕擷取畫面，您需要選取 [將 python.exe 加入路徑]](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* <span data-ttu-id="7ddaa-131">[適用於 Python 2.7 的 Microsoft Visual C++ 編譯器](https://www.microsoft.com/en-us/download/details.aspx?id=44266)。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-131">[Microsoft Visual C++ Compiler for Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="7ddaa-132">步驟 1：建立 Azure Cosmos DB 資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="7ddaa-132">Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="7ddaa-133">我們將從建立 Cosmos DB 帳戶開始著手。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-133">Let's start by creating an Cosmos DB account.</span></span> <span data-ttu-id="7ddaa-134">如果您已經擁有帳戶，或如果您正在使用 Azure Cosmos DB 模擬器來進行本教學課程，可以跳到[步驟 2：建立新的 Python Flask Web 應用程式](#step-2-create-a-new-python-flask-web-application)。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-134">If you already have an account or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Step 2: Create a new Python Flask web application](#step-2-create-a-new-python-flask-web-application).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
<span data-ttu-id="7ddaa-135">我們現在將從頭開始逐步解說如何建立新的 Python Flask Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-135">We will now walk through how to create a new Python Flask web application from the ground up.</span></span>

## <a name="step-2-create-a-new-python-flask-web-application"></a><span data-ttu-id="7ddaa-136">步驟 2：建立新的 Python Flask Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7ddaa-136">Step 2: Create a new Python Flask web application</span></span>
1. <span data-ttu-id="7ddaa-137">在 Visual Studio 的 [檔案] 功能表中，指向 [新增]，然後按一下 [專案]。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-137">In Visual Studio, on the **File** menu, point to **New**, and then click **Project**.</span></span>
   
    <span data-ttu-id="7ddaa-138">[新增專案]  對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-138">The **New Project** dialog box appears.</span></span>
2. <span data-ttu-id="7ddaa-139">在左窗格中，依序展開 [範本]、[Python]，再按一下 [Web]。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-139">In the left pane, expand **Templates** and then **Python**, and then click **Web**.</span></span> 
3. <span data-ttu-id="7ddaa-140">在中央窗格中選取 [Flask Web 專案]，並在 [名稱] 方塊中輸入 [教學課程]，再按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-140">Select **Flask  Web Project** in the center pane, then in the **Name** box type **tutorial**, and then click **OK**.</span></span> <span data-ttu-id="7ddaa-141">請記住，Python 封裝名稱應該全小寫，如 [Python 程式碼文件編寫指南](https://www.python.org/dev/peps/pep-0008/#package-and-module-names)中所述。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-141">Remember that Python package names should be all lowercase, as described in the [Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span></span>
   
    <span data-ttu-id="7ddaa-142">對於 Python Flask 的初學者而言，此 Web 應用程式開發架構可協助您在 Python 中更快速地建置 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-142">For those new to Python Flask, it is a web application development framework that helps you build web applications in Python faster.</span></span>
   
    ![Visual Studio 中左側為反白顯示的 Python、中間為選取的「Python Flask Web 專案」，以及 [名稱] 方塊中名稱為 tutorial 的 [新增專案] 視窗螢幕擷取畫面](./media/documentdb-python-application/image9.png)
4. <span data-ttu-id="7ddaa-144">在 [Python Tools for Visual Studio] 視窗中，按一下 [虛擬環境安裝]。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-144">In the **Python Tools for Visual Studio** window, click **Install into a virtual environment**.</span></span> 
   
    ![資料庫教學課程 - Python Tools for Visual Studio 視窗的螢幕擷取畫面](./media/documentdb-python-application/python-install-virtual-environment.png)
5. <span data-ttu-id="7ddaa-146">在 [加入虛擬環境] 視窗中，接受預設值並使用 Python 2.7 當做基本環境，因為 PyDocumentDB 目前不支援 Python 3.x；接著按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-146">In the **Add Virtual Environment** window, you can accept the defaults and use Python 2.7 as the base environment because PyDocumentDB does not currently support Python 3.x, and then click **Create**.</span></span> <span data-ttu-id="7ddaa-147">這會設定專案所需的 Python 虛擬環境。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-147">This sets up the required Python virtual environment for your project.</span></span>
   
    ![資料庫教學課程 - Python Tools for Visual Studio 視窗的螢幕擷取畫面](./media/documentdb-python-application/image10_A.png)
   
    <span data-ttu-id="7ddaa-149">當成功安裝環境之後，輸出視窗會顯示 `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` 。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-149">The output window displays `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` when the environment is successfully installed.</span></span>

## <a name="step-3-modify-the-python-flask-web-application"></a><span data-ttu-id="7ddaa-150">步驟 3：修改 Python Flask Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7ddaa-150">Step 3: Modify the Python Flask web application</span></span>
### <a name="add-the-python-flask-packages-to-your-project"></a><span data-ttu-id="7ddaa-151">將 Python Flask 封裝加入專案</span><span class="sxs-lookup"><span data-stu-id="7ddaa-151">Add the Python Flask packages to your project</span></span>
<span data-ttu-id="7ddaa-152">專案設定好之後，您需要加入專案所需的特定 Flask 封裝，包括 pydocumentdb (DocumentDB 的 Python 封裝)。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-152">After your project is set up, you'll need to add the required Flask packages to your project, including pydocumentdb, the Python package for DocumentDB.</span></span>

1. <span data-ttu-id="7ddaa-153">在「方案總管」中開啟名為 **requirements.txt** 的檔案，並將其內容取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="7ddaa-153">In Solution Explorer, open the file named **requirements.txt** and replace the contents with the following:</span></span>
   
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
2. <span data-ttu-id="7ddaa-154">儲存 **requirements.txt** 檔案。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-154">Save the **requirements.txt** file.</span></span> 
3. <span data-ttu-id="7ddaa-155">在「方案總管」中以滑鼠右鍵按一下 [env]，然後按一下 [從 requirements.txt 安裝]。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-155">In Solution Explorer, right-click **env** and click **Install from requirements.txt**.</span></span>
   
    ![螢幕擷取畫面，顯示從清單中反白顯示的 requirements.txt 安裝時選取的 env (Python 2.7)。](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    <span data-ttu-id="7ddaa-157">成功安裝之後，輸出視窗會顯示下列資訊：</span><span class="sxs-lookup"><span data-stu-id="7ddaa-157">After successful installation, the output window displays the following:</span></span>
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > <span data-ttu-id="7ddaa-158">在罕見情況下，輸出視窗中可能會出現失敗。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-158">In rare cases, you might see a failure in the output window.</span></span> <span data-ttu-id="7ddaa-159">如果發生此情形，請檢查錯誤是否與清除有關。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-159">If this happens, check if the error is related to cleanup.</span></span> <span data-ttu-id="7ddaa-160">有時是清理失敗，但安裝卻成功 (在輸出視窗中向上捲動來驗證這一點)。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-160">Sometimes the cleanup fails, but the installation will still be successful (scroll up in the output window to verify this).</span></span> <span data-ttu-id="7ddaa-161">您可以 [驗證虛擬環境](#verify-the-virtual-environment)來檢查安裝。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-161">You can check your installation by [Verifying the virtual environment](#verify-the-virtual-environment).</span></span> <span data-ttu-id="7ddaa-162">如果安裝失敗，但驗證成功，則可以繼續。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-162">If the installation failed but the verification is successful, it's OK to continue.</span></span>
   > 
   > 

### <a name="verify-the-virtual-environment"></a><span data-ttu-id="7ddaa-163">驗證虛擬環境</span><span class="sxs-lookup"><span data-stu-id="7ddaa-163">Verify the virtual environment</span></span>
<span data-ttu-id="7ddaa-164">讓我們來確定一切都安裝正確。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-164">Let's make sure that everything is installed correctly.</span></span>

1. <span data-ttu-id="7ddaa-165">按下 **Ctrl**+**Shift**+**B** 建置解決方案。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-165">Build the solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="7ddaa-166">建置成功後，按下 **F5**啟動網站。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-166">Once the build succeeds, start the website by pressing **F5**.</span></span> <span data-ttu-id="7ddaa-167">這會啟動 Flask 開發伺服器和您的網頁瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-167">This launches the Flask development server and starts your web browser.</span></span> <span data-ttu-id="7ddaa-168">應該會出現下列網頁。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-168">You should see the following page.</span></span>
   
    ![在瀏覽器中會顯示空白的 Python Flask Web 開發專案](./media/documentdb-python-application/image12.png)
3. <span data-ttu-id="7ddaa-170">在 Visual Studio 中按 **Shift**+**F5** 停止對網站進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-170">Stop debugging the website by pressing **Shift**+**F5** in Visual Studio.</span></span>

### <a name="create-database-collection-and-document-definitions"></a><span data-ttu-id="7ddaa-171">建立資料庫、集合和文件定義</span><span class="sxs-lookup"><span data-stu-id="7ddaa-171">Create database, collection, and document definitions</span></span>
<span data-ttu-id="7ddaa-172">現在請加入新檔案並更新其他檔案，以建立您的投票應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-172">Now let's create your voting application by adding new files and updating others.</span></span>

1. <span data-ttu-id="7ddaa-173">在「方案總管」中，以滑鼠右鍵按一下 [教學課程] 專案，然後按一下 [加入]，再按一下 [新增項目]。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-173">In Solution Explorer, right-click the **tutorial** project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="7ddaa-174">選取 [空白 Python 檔案]，並將檔案命名為 **forms.py**。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-174">Select **Empty Python File** and name the file **forms.py**.</span></span>  
2. <span data-ttu-id="7ddaa-175">將下列程式碼加入 forms.py 檔案，然後儲存該檔案。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-175">Add the following code to the forms.py file, and then save the file.</span></span>

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-the-required-imports-to-viewspy"></a><span data-ttu-id="7ddaa-176">將必要匯入新增至 views.py</span><span class="sxs-lookup"><span data-stu-id="7ddaa-176">Add the required imports to views.py</span></span>
1. <span data-ttu-id="7ddaa-177">在「方案總管」中，展開 [教學課程] 資料夾，然後開啟 **views.py** 檔案。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-177">In Solution Explorer, expand the **tutorial** folder, and open the **views.py** file.</span></span> 
2. <span data-ttu-id="7ddaa-178">在 **views.py** 檔案頂端新增下列 import 陳述式，然後儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-178">Add the following import statements to the top of the **views.py** file, then save the file.</span></span> <span data-ttu-id="7ddaa-179">這些陳述式會將 Cosmos DB 的 PythonSDK 和 Flask 套件匯入。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-179">These import Cosmos DB's PythonSDK and the Flask packages.</span></span>
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a><span data-ttu-id="7ddaa-180">建立資料庫、集合和文件</span><span class="sxs-lookup"><span data-stu-id="7ddaa-180">Create database, collection, and document</span></span>
* <span data-ttu-id="7ddaa-181">在 **views.py**檔案結尾處加入以下程式碼。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-181">Still in **views.py**, add the following code to the end of the file.</span></span> <span data-ttu-id="7ddaa-182">此程式碼可建立表單所使用的資料庫。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-182">This takes care of creating the database used by the form.</span></span> <span data-ttu-id="7ddaa-183">請勿刪除 **views.py**中任何現有的程式碼。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-183">Do not delete any of the existing code in **views.py**.</span></span> <span data-ttu-id="7ddaa-184">只需將它附加至結尾。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-184">Simply append this to the end.</span></span>

```python
@app.route('/create')
def create():
    """Renders the contact page."""
    client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

    # Attempt to delete the database.  This allows this to be used to recreate as well as create
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


### <a name="read-database-collection-document-and-submit-form"></a><span data-ttu-id="7ddaa-185">讀取資料庫、集合、文件並送出表單</span><span class="sxs-lookup"><span data-stu-id="7ddaa-185">Read database, collection, document, and submit form</span></span>
* <span data-ttu-id="7ddaa-186">在 **views.py**檔案結尾處加入以下程式碼。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-186">Still in **views.py**, add the following code to the end of the file.</span></span> <span data-ttu-id="7ddaa-187">此程式碼可設定表單並讀取資料庫、集合和文件。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-187">This takes care of setting up the form, reading the database, collection, and document.</span></span> <span data-ttu-id="7ddaa-188">請勿刪除 **views.py**中任何現有的程式碼。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-188">Do not delete any of the existing code in **views.py**.</span></span> <span data-ttu-id="7ddaa-189">只需將它附加至結尾。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-189">Simply append this to the end.</span></span>

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

        # Take the data from the deploy_preference and increment our database
        doc[form.deploy_preference.data] = doc[form.deploy_preference.data] + 1
        replaced_document = client.ReplaceDocument(doc['_self'], doc)

        # Create a model to pass to results.html
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


### <a name="create-the-html-files"></a><span data-ttu-id="7ddaa-190">建立 HTML 檔案</span><span class="sxs-lookup"><span data-stu-id="7ddaa-190">Create the HTML files</span></span>
1. <span data-ttu-id="7ddaa-191">在「方案總管」中，以滑鼠右鍵按一下 [教學課程] 資料夾中的 [範本] 資料夾，然後按一下 [新增]，再按一下 [新增項目]。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-191">In Solution Explorer, in the **tutorial** folder, right click the **templates** folder, click **Add**, and then click **New Item**.</span></span> 
2. <span data-ttu-id="7ddaa-192">選取 [HTML 頁面]，在名稱方塊中輸入 **create.html**。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-192">Select **HTML Page**, and then in the name box type **create.html**.</span></span> 
3. <span data-ttu-id="7ddaa-193">重複步驟 1 和 2 來建立其他兩個 HTML 檔案，分別是 results.html 和 vote.html。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-193">Repeat steps 1 and 2 to create two additional HTML files: results.html and vote.html.</span></span>
4. <span data-ttu-id="7ddaa-194">將下列程式碼新增至 `<body>` 元素中的 **create.html**。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-194">Add the following code to **create.html** in the `<body>` element.</span></span> <span data-ttu-id="7ddaa-195">此程式碼可顯示訊息，指出我們已建立新的資料庫、集合和文件。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-195">It displays a message stating that we created a new database, collection, and document.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. <span data-ttu-id="7ddaa-196">將下列程式碼新增至 `<body`> 元素中的 **results.html**。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-196">Add the following code to **results.html** in the `<body`> element.</span></span> <span data-ttu-id="7ddaa-197">此程式碼會顯示投票結果。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-197">It displays the results of the poll.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Results of the vote</h2>
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
6. <span data-ttu-id="7ddaa-198">將下列程式碼新增至 `<body`> 元素中的 **vote.html**。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-198">Add the following code to **vote.html** in the `<body`> element.</span></span> <span data-ttu-id="7ddaa-199">此程式碼會顯示並接受投票。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-199">It displays the poll and accepts the votes.</span></span> <span data-ttu-id="7ddaa-200">註冊投票時，控制權會傳遞給 views.py，我們將在其中辨識投票以及相應地附加文件。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-200">On registering the votes, the control is passed over to views.py where we will recognize the vote cast and append the document accordingly.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>What is your favorite way to host an application on Azure?</h2>
    <form action="" method="post" name="vote">
        {{form.hidden_tag()}}
            {{form.deploy_preference}}
            <button class="btn btn-primary" type="submit">Vote</button>
    </form>
    {% endblock %}
    ```
7. <span data-ttu-id="7ddaa-201">在 [範本] 資料夾中，使用下列程式碼取代 **index.html** 的內容。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-201">In the **templates** folder, replace the contents of **index.html** with the following.</span></span> <span data-ttu-id="7ddaa-202">此程式碼可做為您應用程式的登陸頁面。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-202">This serves as the landing page for your application.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear the Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-the-initpy"></a><span data-ttu-id="7ddaa-203">新增組態檔並變更 \_\_init\_\_.py</span><span class="sxs-lookup"><span data-stu-id="7ddaa-203">Add a configuration file and change the \_\_init\_\_.py</span></span>
1. <span data-ttu-id="7ddaa-204">在「方案總管」中，以滑鼠右鍵按一下 [教學課程] 專案，再依序按一下 [加入]、[新增項目]，接著選取 [空白 Python 檔案]，並為 **config.py** 檔案命名。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-204">In Solution Explorer, right-click the **tutorial** project, click **Add**, click **New Item**, select **Empty Python File**, and then name the file **config.py**.</span></span> <span data-ttu-id="7ddaa-205">Flask 中的表單需要使用此組態檔案。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-205">This config file is required by forms in Flask.</span></span> <span data-ttu-id="7ddaa-206">您也可以用它來提供秘密金鑰。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-206">You can use it to provide a secret key as well.</span></span> <span data-ttu-id="7ddaa-207">但本教學課程不需要用到此金鑰。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-207">This key is not needed for this tutorial though.</span></span>
2. <span data-ttu-id="7ddaa-208">要在 config.py 中新增下列程式碼，您需要在下個步驟中變更 **DOCUMENTDB\_HOST** 和 **DOCUMENTDB\_KEY** 的值。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-208">Add the following code to config.py, you'll need to alter the values of **DOCUMENTDB\_HOST** and **DOCUMENTDB\_KEY** in the next step.</span></span>
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. <span data-ttu-id="7ddaa-209">在 [Azure 入口網站](https://portal.azure.com/)中，按一下 [瀏覽]、[Azure Cosmos DB 帳戶]，按兩下要使用的帳戶名稱，再按一下 [基本功能] 區域中的 [金鑰] 按鈕，可瀏覽至 [金鑰] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-209">In the [Azure portal](https://portal.azure.com/), navigate to the **Keys** blade by clicking **Browse**, **Azure Cosmos DB Accounts**, double-click the name of the account to use, and then click the **Keys** button in the **Essentials** area.</span></span> <span data-ttu-id="7ddaa-210">在 [金鑰] 刀鋒視窗中複製 **URI** 值並貼到 **config.py** 檔案中，做為 **DOCUMENTDB\_HOST** 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-210">In the **Keys** blade, copy the **URI** value and paste it into the **config.py** file, as the value for the **DOCUMENTDB\_HOST** property.</span></span> 
4. <span data-ttu-id="7ddaa-211">回到 Azure 入口網站，在 [金鑰] 刀鋒視窗中複製**主要金鑰**或**次要金鑰**值，貼到 **config.py** 檔案中，做為 **DOCUMENTDB\_KEY** 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-211">Back in the Azure portal, in the **Keys** blade, copy the value of the **Primary Key** or the **Secondary Key**, and paste it into the **config.py** file, as the value for the **DOCUMENTDB\_KEY** property.</span></span>
5. <span data-ttu-id="7ddaa-212">在 **\_\_init\_\_.py** 檔案中，加入以下這一行。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-212">In the **\_\_init\_\_.py** file, add the following line.</span></span> 
   
        app.config.from_object('config')
   
    <span data-ttu-id="7ddaa-213">因此，檔案的內容應該如下：</span><span class="sxs-lookup"><span data-stu-id="7ddaa-213">So that the content of the file is:</span></span>
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. <span data-ttu-id="7ddaa-214">加入所有檔案之後，方案總管看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="7ddaa-214">After adding all the files, Solution Explorer should look like this:</span></span>
   
    ![Visual Studio [方案總管] 視窗的螢幕擷取畫面](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a><span data-ttu-id="7ddaa-216">步驟 4：在本機執行您的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7ddaa-216">Step 4: Run your web application locally</span></span>
1. <span data-ttu-id="7ddaa-217">按下 **Ctrl**+**Shift**+**B** 建置解決方案。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-217">Build the solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="7ddaa-218">建置成功後，按下 **F5**啟動網站。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-218">Once the build succeeds, start the website by pressing **F5**.</span></span> <span data-ttu-id="7ddaa-219">您應該會在畫面上看到下列內容。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-219">You should see the following on your screen.</span></span>
   
    ![網頁瀏覽器中顯示的 Python + Azure Cosmos DB 投票應用程式螢幕擷取畫面](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. <span data-ttu-id="7ddaa-221">按一下 [建立/清除投票資料庫]  來產生資料庫。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-221">Click **Create/Clear the Voting Database** to generate the database.</span></span>
   
    ![Web 應用程式建立頁面 - 開發詳細資訊的螢幕擷取畫面](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. <span data-ttu-id="7ddaa-223">然後，按一下 [投票]  ，並選取您的選項。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-223">Then, click **Vote** and select your option.</span></span>
   
    ![具有投票問題的 Web 應用程式的螢幕擷取畫面](./media/documentdb-python-application/cosmos-db-vote.png)
5. <span data-ttu-id="7ddaa-225">對於您投的每張票，都會讓適當的計數器數字遞增。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-225">For every vote you cast, it increments the appropriate counter.</span></span>
   
    ![顯示投票頁面結果的螢幕擷取畫面](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. <span data-ttu-id="7ddaa-227">按下 Shift+F5 停止對專案進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-227">Stop debugging the project by pressing Shift+F5.</span></span>

## <a name="step-5-deploy-the-web-application-to-azure"></a><span data-ttu-id="7ddaa-228">步驟 5：將 Web 應用程式部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="7ddaa-228">Step 5: Deploy the web application to Azure</span></span>
<span data-ttu-id="7ddaa-229">您已經擁有可在 Cosmos DB 正常運作的完整應用程式，我們現在要將此應用程式部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-229">Now that you have the complete application working correctly against Cosmos DB, we're going to deploy this to Azure.</span></span>

1. <span data-ttu-id="7ddaa-230">以滑鼠右鍵按一下「方案總管」中的專案 (請確定您已沒有在本機上執行該案)，然後選取 [發佈] 。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-230">Right-click the project in Solution Explorer (make sure you're not still running it locally) and select **Publish**.</span></span>  
   
     ![[方案總管] 中選取之教學課程 (具有反白顯示的 [發佈] 選項) 的螢幕擷取畫面](./media/documentdb-python-application/image20.png)
2. <span data-ttu-id="7ddaa-232">在 [發佈] 對話方塊中，選取 [Microsoft Azure App Service]，選取 [新建]，然後按一下 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-232">In the **Publish** dialog box, select **Microsoft Azure App Service**, select **Create New**, and then click **Publish**.</span></span>
   
    ![醒目提示 Microsoft Azure App Service 之 [發佈 Web] 視窗的螢幕擷取畫面](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. <span data-ttu-id="7ddaa-234">在 [建立 App Service] 對話方塊中，輸入您的 Web 應用程式名稱和 [訂用帳戶]、[資源群組]，以及 [App Service 方案]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-234">In the **Create App Service** dialog box, enter the name for your web app along with your **Subscription**, **Resource Group**, and **App Service Plan**, then click **Create**.</span></span>
   
    ![[Microsoft Azure Web Apps 視窗] 視窗的螢幕擷取畫面](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. <span data-ttu-id="7ddaa-236">幾秒後，Visual Studio 將完成發佈 App Service 並啟動瀏覽器，您可以在瀏覽器中看到您方便好用的應用程式已在 Azure 中執行！</span><span class="sxs-lookup"><span data-stu-id="7ddaa-236">In a few seconds, Visual Studio will finish publishing your app service and launch a browser where you can see your handiwork running in Azure!</span></span>

    ![[Microsoft Azure Web Apps 視窗] 視窗的螢幕擷取畫面](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a><span data-ttu-id="7ddaa-238">疑難排解</span><span class="sxs-lookup"><span data-stu-id="7ddaa-238">Troubleshooting</span></span>
<span data-ttu-id="7ddaa-239">如果這是您在電腦上執行的第一個 Python 應用程式，請確定 PATH 變數中包括下列資料夾 (或同等的安裝位置：</span><span class="sxs-lookup"><span data-stu-id="7ddaa-239">If this is the first Python app you've run on your computer, ensure that the following folders (or the equivalent installation locations) are included in your PATH variable:</span></span>

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

<span data-ttu-id="7ddaa-240">如果您在投票頁面上收到錯誤，且您的專案不是命名為**教學課程**，請確定 **\_\_init\_\_.py** 在下列程式碼行中參照了正確的專案名稱：`import tutorial.view`。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-240">If you receive an error on your vote page, and you named your project something other than **tutorial**, make sure that **\_\_init\_\_.py** references the correct project name in the line: `import tutorial.view`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ddaa-241">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7ddaa-241">Next steps</span></span>
<span data-ttu-id="7ddaa-242">恭喜！</span><span class="sxs-lookup"><span data-stu-id="7ddaa-242">Congratulations!</span></span> <span data-ttu-id="7ddaa-243">您剛剛已使用 Cosmos DB 建置您的第一個 Python Web 應用程式，並將它發佈至 Azure。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-243">You have just completed your first Python web application using Cosmos DB and published it to Azure.</span></span>

<span data-ttu-id="7ddaa-244">我們會根據您的意見反應，經常更新並改善此主題。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-244">We update and improve this topic frequently based on your feedback.</span></span>  <span data-ttu-id="7ddaa-245">當您完成教學課程後，請使用位於此頁面頂端及底部的投票按鈕來投票，並務必對您想看到的改善內容提供您的意見反應。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-245">Once you've completed the tutorial, please using the voting buttons at the top and bottom of this page, and be sure to include your feedback on what improvements you want to see made.</span></span> <span data-ttu-id="7ddaa-246">如果想要我們直接與您連絡，歡迎在留言中留下電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-246">If you'd like us to contact you directly, feel free to include your email address in your comments.</span></span>

<span data-ttu-id="7ddaa-247">若要在 Web 應用程式中加入其他功能，請檢閱 [Azure Cosmos DB Python SDK](documentdb-sdk-python.md) 中可用的 API。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-247">To add additional functionality to your web application, review the APIs available in the [Azure Cosmos DB Python SDK](documentdb-sdk-python.md).</span></span>

<span data-ttu-id="7ddaa-248">如需 Azure、Visual Studio 及 Python 的詳細資訊，請參閱 [Python 開發人員中心](https://azure.microsoft.com/develop/python/)。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-248">For more information about Azure, Visual Studio, and Python, see the [Python Developer Center](https://azure.microsoft.com/develop/python/).</span></span> 

<span data-ttu-id="7ddaa-249">如需其他的 Python Flask 教學課程，請參閱 [Flask 教學課程庫，第一部分：Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world)。</span><span class="sxs-lookup"><span data-stu-id="7ddaa-249">For additional Python Flask tutorials, see [The Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span></span> 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com
