### <a name="prerequisites"></a>必要條件
* Twilio 帳戶
* 已驗證的 Twilio 電話號碼，以便接收簡訊
* 已驗證的 Twilio 電話號碼，以便傳送簡訊

> [!NOTE]
> 如果您使用的 Twilio 試用版帳戶，您可以只傳送 SMS 太**驗證**電話號碼。  
> 
> 

您可以在邏輯應用程式中使用 Twilio 帳戶之前，您必須授權 hello 邏輯應用程式 tooconnect tooyour Twilio 帳戶。 幸運的是，您可以輕鬆地在 hello Azure 入口網站上的應用程式邏輯中。 

以下是您的邏輯應用程式 tooconnect tooyour Twilio 帳戶 hello 步驟 tooauthorize:

1. toocreate 連接 tooTwilio，在 hello 邏輯應用程式設計師中，選取**顯示 Microsoft managed Api** hello 在下拉式清單，然後輸入*Twilio* hello [搜尋] 方塊中。 選取 hello 觸發程序或您一定會喜歡 toouse 的動作：  
   ![](./media/connectors-create-api-twilio/twilio-0.png)
2. 如果您尚未建立任何連線 tooTwilio 之前，您會取得提示的 tooprovide Twilio 認證。 這些認證會使用的 tooauthorize，您的邏輯應用程式 tooconnect 並存取您的 Twilio 帳戶資料：  
   ![](./media/connectors-create-api-twilio/twilio-1.png)  
3. 您將需要 hello **Twilio 帳戶識別碼**和**Twilio 存取權杖**hello 儀表板中 Twilio 因此登入 tooyour Twilio 帳戶現在 toograb 這兩個資訊片段：  
   ![](./media/connectors-create-api-twilio/twilio-2.png)  
4. Twilio 和邏輯的應用程式使用不同的名稱 tooidentify 這兩個資訊片段。 以下是如何您必須將其對應 toohello 邏輯應用程式 對話方塊：![](./media/connectors-create-api-twilio/twilio-3.png)  
5. 選取 hello**建立連線**按鈕：  
   ![](./media/connectors-create-api-twilio/twilio-4.png)
6. 請注意，已經建立 hello 連接，而且現在可用以 hello 其他 tooproceed 邏輯應用程式中的步驟：  
   ![](./media/connectors-create-api-twilio/twilio-5.png)

