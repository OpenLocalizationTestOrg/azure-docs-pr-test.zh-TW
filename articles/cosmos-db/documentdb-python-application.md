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
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a>使用 Azure Cosmos DB 建置 Python Flask Web 應用程式
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

本教學課程會示範如何 toouse Azure Cosmos DB toostore 及存取資料來自 Python web 應用程式裝載於 Azure，並假設您有一些使用經驗，使用 Python 和 Azure 網站。

此資料庫教學課程涵蓋：

1. 建立和佈建 Cosmos DB 帳戶。
2. 建立 Python Flask 應用程式。
3. 連接 web 應用程式使用 Cosmos DB tooand。
4. 部署的 hello web 應用程式 tooAzure。

遵循此教學課程中，您將建立簡單的投票應用程式，可讓您輪詢的 toovote。

![建立此資料庫教學課程中的 hello 投票應用程式的螢幕擷取畫面](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a>資料庫教學課程必要條件
這篇文章中的 hello 指示之前，您應該確定您擁有 hello 安裝下列項目：

* 使用中的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
 
    或 

    Hello 的本機安裝[Azure Cosmos DB 模擬器](local-emulator.md)。
* [Microsoft Visual Studio Community 2017](http://www.visualstudio.com/)。  
* [Python Tools for Visual Studio](https://github.com/Microsoft/PTVS/)。  
* [Microsoft Azure SDK for Python 2.7](https://azure.microsoft.com/downloads/)。 
* [Python 2.7.13](https://www.python.org/downloads/windows/)。 

> [!IMPORTANT]
> 如果您要安裝 Python 2.7 hello 第一次，請確定在 hello 自訂 Python 2.7.13 畫面中，您選取**新增 python.exe tooPath**。
> 
> ![Hello 自訂 Python 2.7.11 畫面上，您需要 tooselect 新增 python.exe tooPath 的螢幕擷取畫面](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* [適用於 Python 2.7 的 Microsoft Visual C++ 編譯器](https://www.microsoft.com/en-us/download/details.aspx?id=44266)。

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a>步驟 1：建立 Azure Cosmos DB 資料庫帳戶
我們將從建立 Cosmos DB 帳戶開始著手。 如果您已經有帳戶，或如果您使用 hello Azure Cosmos DB 模擬器本教學課程中，您可以跳過[步驟 2： 建立新的 Python 酒瓶 web 應用程式](#step-2-create-a-new-python-flask-web-application)。

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
我們現在將逐步引導 toocreate 新的 Python 酒瓶 web 應用程式，從 hello 地面的方式。

## <a name="step-2-create-a-new-python-flask-web-application"></a>步驟 2：建立新的 Python Flask Web 應用程式
1. 在 Visual Studio 中的 hello**檔案**功能表上，點太**新增**，然後按一下**專案**。
   
    hello**新專案** 對話方塊隨即出現。
2. Hello 左窗格中，展開 **範本**然後**Python**，然後按一下 **Web**。 
3. 選取**酒瓶 Web 專案**hello 中央窗格中，然後在 hello**名稱**方塊中，輸入**教學課程**，然後按一下**確定**。 請記住，hello 中所述，Python 封裝名稱應該是全部小寫， [Python 程式碼的樣式指南](https://www.python.org/dev/peps/pep-0008/#package-and-module-names)。
   
    這些新 tooPython 酒瓶，對於 web 應用程式開發架構，可協助您以 Python web 應用程式的建立更為快速。
   
    ![在 Visual Studio 中使用 Python 上左、 Python 酒瓶 Web 專案 hello 名稱方塊中選取 hello 中間和 hello 名稱教學課程中的 hello 反白顯示 hello [新增專案] 視窗的螢幕擷取畫面](./media/documentdb-python-application/image9.png)
4. 在 hello **Python Tools for Visual Studio**視窗中，按一下 **安裝在虛擬環境**。 
   
    ![Hello database 教學課程-Python Tools for Visual Studio 視窗的螢幕擷取畫面](./media/documentdb-python-application/python-install-virtual-environment.png)
5. 在 hello**加入虛擬環境**視窗中，您可以接受 hello 預設值，並使用 Python 2.7 hello 基底的環境，因為 PyDocumentDB 目前不支援 Python 3.x 中，然後再按一下**建立**。 這會設定為您的專案所需的 hello Python 虛擬環境。
   
    ![Hello database 教學課程-Python Tools for Visual Studio 視窗的螢幕擷取畫面](./media/documentdb-python-application/image10_A.png)
   
    hello 輸出 視窗會顯示`Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.`hello 環境已成功安裝。

## <a name="step-3-modify-hello-python-flask-web-application"></a>步驟 3： 修改 hello Python 酒瓶 web 應用程式
### <a name="add-hello-python-flask-packages-tooyour-project"></a>加入 hello Python 酒瓶封裝 tooyour 專案
您的專案設定後，您需要 tooadd 所需的 hello 酒瓶封裝 tooyour 專案，包括 pydocumentdb，DocumentDB 的 hello Python 封裝。

1. 在 [方案總管] 中，開啟名為 hello 檔案**requirements.txt**並取代 hello 下列中的 hello 內容：
   
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
2. 儲存 hello **requirements.txt**檔案。 
3. 在「方案總管」中以滑鼠右鍵按一下 [env]，然後按一下 [從 requirements.txt 安裝]。
   
    ![螢幕擷取畫面顯示 env (Python 2.7) 從 requirements.txt hello 清單中反白顯示所選取的安裝](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    安裝成功後，hello [輸出] 視窗會顯示 hello 下列：
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > 在罕見的情況下，您可能會看到 hello [輸出] 視窗中的失敗。 如果發生這種情況，請檢查 hello 錯誤是否相關的 toocleanup。 有時 hello 清除會失敗，但是 hello 安裝仍然會成功 （向上捲動 hello 輸出視窗 tooverify 這）。 您可以檢查您安裝[確認 hello 虛擬環境](#verify-the-virtual-environment)。 如果 hello 安裝失敗，但 hello 驗證會成功，則確定 toocontinue。
   > 
   > 

### <a name="verify-hello-virtual-environment"></a>確認 hello 虛擬環境
讓我們來確定一切都安裝正確。

1. 按建置 hello 方案**Ctrl**+**Shift**+**B**。
2. Hello 建置成功後，請按下啟動 hello 網站**F5**。 這會啟動 hello 酒瓶程式開發伺服器，並啟動 web 瀏覽器。 您應該會看到下列頁面的 hello。
   
    ![hello 空 Python 酒瓶的 web 開發專案在瀏覽器](./media/documentdb-python-application/image12.png)
3. 停止偵錯 hello 網站按**Shift**+**F5** Visual Studio 中。

### <a name="create-database-collection-and-document-definitions"></a>建立資料庫、集合和文件定義
現在請加入新檔案並更新其他檔案，以建立您的投票應用程式。

1. 在 方案總管 中，以滑鼠右鍵按一下 hello**教學課程**專案中，按一下 **新增**，然後按一下**新項目**。 選取**空的 Python 檔案**和名稱 hello 檔案**forms.py**。  
2. 新增下列程式碼 toohello forms.py 檔案中的 hello，然後將檔案儲存 hello。

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-hello-required-imports-tooviewspy"></a>加入所需的 hello 匯入 tooviews.py
1. 在 方案總管 中，展開 hello**教學課程**資料夾，然後開啟 hello **views.py**檔案。 
2. 新增下列匯入陳述式 toohello hello 頂端的 hello **views.py**檔案，然後儲存 hello 檔案。 這些匯入 Cosmos DB PythonSDK 和 hello 酒瓶封裝。
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a>建立資料庫、集合和文件
* 仍在**views.py**，加入下列程式碼 toohello 結尾 hello 檔案 hello。 這會負責建立 hello hello 表單所使用的資料庫。 請勿刪除任何現有的程式碼 hello 中**views.py**。 只是附加此 toohello 結束。

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


### <a name="read-database-collection-document-and-submit-form"></a>讀取資料庫、集合、文件並送出表單
* 仍在**views.py**，加入下列程式碼 toohello 結尾 hello 檔案 hello。 這會負責設定 hello 形式，讀取 hello 資料庫、 集合和文件。 請勿刪除任何現有的程式碼 hello 中**views.py**。 只是附加此 toohello 結束。

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


### <a name="create-hello-html-files"></a>建立 hello HTML 檔案
1. 在 方案總管中 hello**教學課程**資料夾中，右邊按一下 hello**範本**資料夾中，按一下 **新增**，然後按一下**新項目**。 
2. 選取**HTML 網頁**，然後在 [hello] 名稱方塊中鍵入**create.html**。 
3. 重複步驟 1 和 2 toocreate 兩個其他的 HTML 檔案： results.html 和 vote.html。
4. 新增下列程式碼太 hello**create.html**在 hello`<body>`項目。 此程式碼可顯示訊息，指出我們已建立新的資料庫、集合和文件。
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. 新增下列程式碼太 hello**results.html**在 hello `<body`> 項目。 它會顯示 hello 輪詢 hello 結果。
   
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
6. 新增下列程式碼太 hello**vote.html**在 hello `<body`> 項目。 它會顯示 hello 輪詢，並接受 hello 投票。 在註冊 hello 投票，hello 控制權會傳遞透過 tooviews.py 我們將在此辨識 hello 投票轉換，並據以附加 hello 文件。
   
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
7. 在 hello**範本**資料夾，取代 hello 內容**index.html** hello 下列。 這可做為 hello 登陸頁面，您的應用程式。
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear hello Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-hello-initpy"></a>加入組態檔並變更 hello \_ \_init\_\_.py
1. 在 方案總管 中，以滑鼠右鍵按一下 hello**教學課程**專案中，按一下 **新增**，按一下**新項目**，選取**空的 Python 檔案**，然後名稱 hello 檔**config.py**。 Flask 中的表單需要使用此組態檔案。 您可以使用 tooprovide 以及祕密金鑰。 但本教學課程不需要用到此金鑰。
2. 將 hello 面一行加入程式碼 tooconfig.py，您將需要 tooalter hello 值**DOCUMENTDB\_主機**和**DOCUMENTDB\_金鑰**hello 下一個步驟中。
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. 在 hello [Azure 入口網站](https://portal.azure.com/)，瀏覽 toohello**金鑰**刀鋒視窗中的按一下**瀏覽**， **Azure Cosmos DB 帳戶**，連按兩下 hello 名稱hello 的帳戶 toouse，，然後按一下hello**金鑰**按鈕在 hello **Essentials**區域。 在 hello**金鑰**刀鋒視窗，複製 hello **URI**值並貼到 hello **config.py**檔案，做為 hello 的 hello 值**DOCUMENTDB\_主機**屬性。 
4. Hello hello 中的 Azure 入口網站中**金鑰**刀鋒視窗中，複製 hello 值 hello**主索引鍵**或 hello**次要金鑰**，並將它貼到 hello **config.py**檔案，做為 hello 的 hello 值**DOCUMENTDB\_金鑰**屬性。
5. 在 hello  **\_ \_init\_\_.py** file、 add hello 行下。 
   
        app.config.from_object('config')
   
    使 hello hello 檔案內容：
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. 加入所有 hello 檔案之後, 方案總管 中看起來應該像這樣：
   
    ![Hello Visual Studio 方案總管 視窗的螢幕擷取畫面](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a>步驟 4：在本機執行您的 Web 應用程式
1. 按建置 hello 方案**Ctrl**+**Shift**+**B**。
2. Hello 建置成功後，請按下啟動 hello 網站**F5**。 您應該會看到下列 hello 螢幕上。
   
    ![Hello Python + Azure Cosmos DB 投票應用程式在 web 瀏覽器中顯示的螢幕擷取畫面](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. 按一下**建立/清除 hello 投票資料庫**toogenerate hello 資料庫。
   
    ![螢幕擷取畫面的 hello 建立網頁的 hello web 應用程式 – 開發的詳細資訊](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. 然後，按一下 [投票]  ，並選取您的選項。
   
    ![Hello 投票問題所造成的 web 應用程式的螢幕擷取畫面](./media/documentdb-python-application/cosmos-db-vote.png)
5. 為您轉換每個投票，它會遞增 hello 適當的計數器。
   
    ![Hello 結果所示的 hello 投票頁面的螢幕擷取畫面](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. 停止偵錯 hello 專案藉由按下 Shift + F5。

## <a name="step-5-deploy-hello-web-application-tooazure"></a>步驟 5： 部署的 hello web 應用程式 tooAzure
既然您已針對 Cosmos DB 正常運作的 hello 完整應用程式時，我們 toodeploy 此 tooAzure。

1. 以滑鼠右鍵按一下方案總管 中的 hello 專案 (請確定您不是仍在本機執行)，選取**發行**。  
   
     ![Hello 教學課程的螢幕擷取畫面中選取方案總管 中，以 hello 反白顯示的 發佈 選項](./media/documentdb-python-application/image20.png)
2. 在 hello**發行**對話方塊中，選取**Microsoft Azure App Service**，選取**建立新**，然後按一下**發行**。
   
    ![使用 Microsoft Azure App Service 反白顯示 hello 發行 Web 視窗的螢幕擷取畫面](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. 在 hello**建立 App Service**對話方塊方塊中，輸入您的 web 應用程式，連同 hello 名稱您**訂用帳戶**，**資源群組**，和**App Service 方案**，然後按一下 **建立**。
   
    ![Microsoft Azure Web 應用程式視窗 [hello] 視窗的螢幕擷取畫面](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. 幾秒後，Visual Studio 將完成發佈 App Service 並啟動瀏覽器，您可以在瀏覽器中看到您方便好用的應用程式已在 Azure 中執行！

    ![Microsoft Azure Web 應用程式視窗 [hello] 視窗的螢幕擷取畫面](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a>疑難排解
如果這是您已在電腦執行 hello 第一個 Python 應用程式，請確定該 hello 下列資料夾 （或 hello 對等的安裝位置） 都包含在 PATH 變數：

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

如果您收到錯誤訊息上投票，而且您命名為您的專案名稱以外**教學課程**，請確定 **\_ \_init\_\_.py**參考 hello hello 行正確的專案名稱： `import tutorial.view`。

## <a name="next-steps"></a>後續步驟
恭喜！ 您剛完成第一個 Python web 應用程式使用 Cosmos DB 並發佈它 tooAzure。

我們會根據您的意見反應，經常更新並改善此主題。  一次您已經完成 hello 教學課程中，請使用 hello 投票按鈕 hello 頂端和底端的這個頁面上，而且確定 tooinclude 上您想要的 toosee 進行何種改善您的意見反應。 如果您希望我們 toocontact 您直接，認為您的電子郵件地址可用 tooinclude 註解中。

tooadd 額外的功能 tooyour web 應用程式中，檢閱 hello Api 可在 hello [Azure Cosmos DB Python SDK](documentdb-sdk-python.md)。

如需有關 Azure 中，Visual Studio 和 Python 的詳細資訊，請參閱 hello [Python 開發人員中心](https://azure.microsoft.com/develop/python/)。 

如需其他的 Python 酒瓶教學課程，請參閱[hello 酒瓶百萬-教學課程中，部分 i: Hello，World ！](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world)。 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com
