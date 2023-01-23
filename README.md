# Wind_project

## status updates

[finding_noisepollution](https://github.com/Jasper-Hewitt/Wind_project/blob/main/finding_noisepollution.ipynb) is the main notebook. I'm currently testing the code on 16 pages that I dragged from the original pdf. I took the pages 130 to 146. 

The summary that chatGPT made is: 結： 本計畫關於噪音的規格已改變，不再使用聲音驅離裝置(ADD)，水下噪音監測的目的決定了打樁工程應採緩啟動(softstart)持續至少30分鐘，並在施工期間於距離打樁位置外750公尺處選擇合理方式來監控噪音水平，以確保噪音不會達到極端高值，達到環境保護。

the prompt that I gave it is: 幫我寫總結之下的內容，強調關於噪音的規格的改變，請你使用比較簡單的語言，小孩子也可以看得懂。

The model is very good at detecting the sentences that have something to do with 噪音. I read and highlighted the document and looked up their position in the df after the sentiment search. In [this document](https://github.com/Jasper-Hewitt/Wind_project/blob/main/data/verified_dragged_130_146.pdf) I analysed pages 130 to 146, highlighted all the parts that had something to do with 噪音, and wrote down what score our model gave to all the highlighted parts. 

sentences with a direct relation came in on the indexes: 
0, 1, 2, 3, 4, 5, 6, 7, 8, 10, 11

Indirect vaguely related to construction and its impact on the fish (but not necessarily about noise pollution)
18, 19, 22, 23, 51


If we need text to remain in the same order in order for GPT to write a proper chronological summary we can consider adding an column to the database that assigns a sentence number to each piece of text based on their original position in the text. If we find out that two sentences that are related to 噪音 have consecutive sentence numbers, for example, sentence 50 and 51 both score a really high overall_score, we can then merge these two sentences back together. That way GPT might find it easier to write a proper summary. 


## todo


- check why the len of sentence_score is only half of that of split_contents. Maybe I'm losing a lot of sentences here. 
- determine a threshold. What overal_score is high enough to assume this sentence has something to do with 噪音.

### done 

- read and highlight the actual pdf and see if the model gets it right
    - see [this document](https://github.com/Jasper-Hewitt/Wind_project/blob/main/data/highlights_dragged_130_146.pdf) for a version of the PDF that highlighted all the parts that have something to do with 噪音
- count the total number of words after converting and check how many was lost.
    - no loss. number of words after copy pasting pdf into word: 8373... after converting with flitz: 8378
- figure out what that warning is: cannot find model with this name... Maybe it's not really using the model now. Otherwise check for other models. 
    - The model that I was trying to use: shibing624/text2vec-base-chinese was not available somehow. I now use another model, see information below. 
    - see if I can assign a column to the df that shows a certain piece of text's sentence number in the original document. (this may be tricky). 

## model

The models below all read Chinese. it looks like the first one was only fine-tuned on simplified Chinese, whereas the second one was also fine-tuned on traditional Chinese. See https://www.sbert.net/docs/pretrained_models.html#multi-lingual-models and the corresponding Hugging Face pages for more information. 

We currently use: sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2.

other option (slightly better performance): https://huggingface.co/sentence-transformers/paraphrase-multilingual-mpnet-base-v2 

There are a few other models like ('shibing624/text2vec-base-chinese') that appear to have good performance, but I have trouble importing them.  

## converting the data
I found that the Fitz package appears to work well enough to convert most of the pdf to text. However, it is unable to read some of the scanned documents on the first few pages of the PDF. I haven't tried to see if it works on all the pages with the pictures.

```import fitz

doc = fitz.open("small_version2.pdf")

for page in doc:
    text = page.get_text("text")
    with open("output3.txt", "a") as f:
        f.write(text)
```

     

## links and references
code is based on: https://www.sbert.net/examples/applications/semantic-search/README.html

For semantic research using open AI API, see: 

see also: https://www.youtube.com/watch?v=ocxq84ocYi0 
