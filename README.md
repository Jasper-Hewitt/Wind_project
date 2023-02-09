# Wind_project

## status updates

- try the query the answer for questions: (0)第327次會議是什麼時候？(1) 第327次會議中，對於鯨豚保育的重點是什麼？(2) 第327次會議中，有哪些專家為鯨豚保育發言？

answers from [1_by_1_mom_327.ipynb](https://github.com/Jasper-Hewitt/Wind_project/blob/main/1_by_1_mom_327.ipynb):

        第327次會議是什麼時候？ 
        第327次會議是107年2月9日（星期五）下午4時30分。


        第327次會議中，對於鯨豚保育的重點是什麼？」 
        答：第327次會議中，對於鯨豚保育的重點是加強監督開發單位對鯨豚之觀測；確定每年30趟鯨豚調查作業；
        施工船上設有至少3位以上鯨豚觀測員（其中至少1位為民間生態團體成員）；
        納入緩衝帶規劃，而基座位址距離中華白海豚野生動物重要棲息環境1,000公尺以上；
        就施工前使用聲音驅趕裝置，暫時驅趕中華白海豚族群等保育類野生動物之規劃，暫緩採用；使用管架式(Jacket)基礎，納入鯨豚減輕對策；
        施工前應先確認至少30分鐘無鯨豚活動後方得作業；施工過程若周界750公尺內有海


        第327次會議中，有哪些專家為鯨豚保育發言？維持如何？請再確認  」
        答覆會議上發言的專家包括劉委員希平、劉委員小如意、鄭委員明修。

output after asking ChatGPT to summarize the answers in one piece of text:
        
         劉委員希平、劉委員小如意、鄭委員明修將出席107年2月9日（星期五）下午4時30分舉行的第327次會議，
         討論與鯨豚保育有關的重點議題，包括：加強監督開發單位對鯨豚之觀測；確定每年30趟鯨豚調查作業；
         施工船上設有至少3位以上鯨豚觀測員（其中至少1位為民間生態團體成員）；
         納入緩衝帶規劃，而基座位址距離中華白海豚野生動物重要棲息環境1,000公尺以上；
         就施工前使用聲音驅趕裝置，暫時驅趕中華白海豚族群等野生動物之規劃，暫緩採用；
         使用管架式(Jacket)基礎，納入鯨豚減輕對策；施工前應先確認至少30分鐘無鯨豚活動後方得作業；施工過程若周界750公尺內有海。
        

Notes on [1_by_1_mom_327.ipynb](https://github.com/Jasper-Hewitt/Wind_project/blob/main/1_by_1_mom_327.ipynb):
- I adopt a new one-by-one approach. Instead of inserting all three questions in the Sbert query at once, I query Sbert one question 
at a time. This leads to better search results that ChatGPT can then use to answer the question.
- As Owen suggested, I no longer query Sbert with keywords but directly insert the question. I then ask ChatGPT the same question.
- dynamic treshold: We were thinking about using Sbert to assess ChatGPT's output and adjust the threshold accordingly. However,
I think we will still run into the same problem as before, what tensor is high enough to accept? I therefore came up with an 
alternative approach. The code below basically selects the maximum number of sentences that Chatgpt accepts (4000 tokens = ~1750 
characters). This way we can assume that the answer should be within the prompt we give ChatGPT and leave it to ChatGPT to filter out 
the answer. 
- it is important to remember that ChatGPT's output is different everytime you prompt it. The quality of the output varies
significantly between answers. 
    
```
# Find the number of characters in each row of the text column
df['text_length'] = df['text'].str.len()

# Get the cumulative sum of the text lengths
df['cumulative_length'] = df['text_length'].cumsum()

# Find the index of the first row in which the cumulative length is greater than 3600
index = df.index[df['cumulative_length'] > 1500][0]

# Create a new dataframe with only the last few rows
new_df = df.iloc[index:]

# Drop the last few rows from the original dataframe
df = df.iloc[:index]
```

### todo
- re-insert the answers into chatGPT and ask it to summarize the answers into one cohesive summary.
- read article on judging GPT summaries (dashboard).
- check the gitignore thing https://git-scm.com/docs/gitignore 
- play around with different prompts, see if results get any better.

**optional adjustments:** 
- try to drop "第327次會議中" from the last two questions and see what the results are. 
- use different queries for Sbert

### alternative outputs

[mom_327_queries1.ipynb](https://github.com/Jasper-Hewitt/Wind_project/blob/main/mom_327_queries1.ipynb): uses 鯨豚, 噪音, and 保育 as keywords （all keywords at once） and asks the direct questions to chat gpt.

output: 
    
    第327次會議是什麼時候？，明文規定於施工前暫時驅趕中華白海豚族群等保育類野生動物之規劃，恐衍生疑慮，
    建議暫緩採用，宜審慎蒐集案例研析後再行考量。

    第327次會議時間不明，請參考主辦單位提供的會議相關資訊以確定會議時間。
    第327次會議中，對於鯨豚保育的重點是什麼？ 之『增設具減噪功能之風機打樁技術』，以維護海洋環境及調節鯨豚行為

    第327次會議中，對於鯨豚保育的重點是採取審慎蒐集案例研析後再行考量、採用較嚴格之噪音管制規範、配備觀察船及配置鯨豚生態觀察員、
    加強監督開發單位對於鯨豚之觀測、採行緩啟動並持續使用最佳噪音防制工法、以及每年30趟次之鯨豚生態調查。
    第327次會議中，有哪些專家為鯨豚保育發言？、禁區內為觀測鯨豚浮游及游泳活動方便，確保每個禁區可循環暢行之艇，以確保正常觀測工作

    第327次會議中專家為鯨豚保育發言的有：

        1. 劉委員小如意
        2. 劉委員希平
        3. 經濟部能源局

[mom_327_queries2.ipynb](https://github.com/Jasper-Hewitt/Wind_project/blob/main/mom_327_queries2.ipynb) asks the questions directly to sbert （all three at once）, and then asks them again to ChatGPT.

output: 

       第327次會議是什麼時候？
       ，意見以上結論至施工當案承辦單位與本署環境影響評估討論會議後盡量於評估期間概算明細內預留資源已投入第三方監測之費用，
       於預算與爭議兩途徑中求解本署環境影響評估審查委員會  第 327 次會議紀錄。
       
       第327次會議中，對於鯨豚保育的重點是什麼？，訂定應監測之項目如下：
       （a） 建立及強化鯨豚觀測員訓練作業，藉由訓練及教育活動提升環境保護工作素養； 
       （b） 應採每年 30 趟次（非僅限於 4～9 月執行，調整前應依法申請變更）之鯨豚生態調查頻率，
       建議邀民間團體具鯨豚觀測能力人員共同參與。  
       答案：第327次會議中，對於鯨豚保育的重點是建立及強化鯨豚觀測員訓練作業，針對施工作業應採每年30趟次的鯨豚生態調查頻率，
       邀請民間團體具有鯨豚觀測能力人員共同參與。
       
       第327次會議中，有哪些專家為鯨豚保育發言？
       ，其觀測內容包括施工處於 1,500 公尺內外側風場發現鯨豚活動之憑盤視察、
       定期水中哺乳類調查，以及對哺乳類之解說等事項，建議應採每年 30 趟次（非僅限於 4～9 月執行，調整前應依法申請變更），
       建議強化鯨豚觀測員訓練作業，並考慮邀民間團體具鯨豚觀測能力人員共同參與 

       第327次會議專家為鯨豚保育發言的有：

        1. 經濟部能源局參與者
        2. 彰化縣線西鄉公所參與者
        3. 行政院農業委員會野生動物保育法訂定者
        4. 環境影響評估書件記載者
        5. 劉委員小如參與者
        6.

## older updates

[finding_noisepollution](https://github.com/Jasper-Hewitt/Wind_project/blob/main/finding_noisepollution.ipynb) is the main notebook. I'm currently testing the code on 16 pages that I dragged from the original pdf. I took the pages 130 to 146. 

The summary that chatGPT made is: 結： 本計畫關於噪音的規格已改變，不再使用聲音驅離裝置(ADD)，水下噪音監測的目的決定了打樁工程應採緩啟動(softstart)持續至少30分鐘，並在施工期間於距離打樁位置外750公尺處選擇合理方式來監控噪音水平，以確保噪音不會達到極端高值，達到環境保護。

the prompt that I gave it is: 幫我寫總結之下的內容，強調關於噪音的規格的改變，請你使用比較簡單的語言，小孩子也可以看得懂。

The model is very good at detecting the sentences that have something to do with 噪音. I read and highlighted the document and looked up their position in the df after the sentiment search. In [this document](https://github.com/Jasper-Hewitt/Wind_project/blob/main/data/verified_dragged_130_146.pdf) I manually analysed pages 130 to 146, highlighted all the parts that had something to do with 噪音, and wrote down what score our model gave to all the highlighted parts. 

sentences with a direct relation came in on the indexes: 
0, 1, 2, 3, 4, 5, 6, 7, 8, 10, 11

Sentences with loose and vague reference to construction its impact on sealife (but not necessarily about noise pollution):
18, 19, 22, 23, 51 

## model

The models below all read Chinese. it looks like the first one was only fine-tuned on simplified Chinese, whereas the second one was also fine-tuned on traditional Chinese. See https://www.sbert.net/docs/pretrained_models.html#multi-lingual-models and the corresponding Hugging Face pages for more information. 

We currently use: sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2.

other option (slightly better performance): https://huggingface.co/sentence-transformers/paraphrase-multilingual-mpnet-base-v2 

There are a few other models like ('shibing624/text2vec-base-chinese') that appear to have good performance, but I have trouble importing them.  
 

## links and references
code is based on: https://www.sbert.net/examples/applications/semantic-search/README.html

For semantic research using open AI API, see: 

see also: https://www.youtube.com/watch?v=ocxq84ocYi0 



### previous steps 

- read and highlight the actual pdf and see if the model gets it right
    - see [this document](https://github.com/Jasper-Hewitt/Wind_project/blob/main/data/highlights_dragged_130_146.pdf) for a version of the PDF that highlighted all the parts that have something to do with 噪音
- count the total number of words after converting and check how many was lost.
    - no loss. number of words after copy pasting pdf into word: 8373... after converting with flitz: 8378
- figure out what that warning is: cannot find model with this name... Maybe it's not really using the model now. Otherwise check for other models. 
    - The model that I was trying to use: shibing624/text2vec-base-chinese was not available somehow. I now use another model, see information below. 
    - see if I can assign a column to the df that shows a certain piece of text's sentence number in the original document. (this may be tricky). 
