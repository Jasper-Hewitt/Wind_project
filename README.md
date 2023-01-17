# Wind_project

## status updates

I'm currently testing the code on 16 pages that I dragged from the original pdf. I took the pages 130 to 146. 

it appears to work: see finding_noisepollution. 

## todo

- read and highlight the actual pdf and see if the model gets it right
- check why the len of sentence_score is only half of that of split_contents. Maybe I'm losing a lot of sentences here. 
- determine a threshold. What overal_score is high enough to assume this sentence has something to do with 噪音.

### done 

- count the total number of words after converting and check how many was lost.
    - no loss. number of words after copy pasting pdf into word: 8373... after converting with flitz: 8378
- figure out what that warning is: cannot find model with this name... Maybe it's not really using the model now. Otherwise check for other models. 
    - The model that I was trying to use: shibing624/text2vec-base-chinese was not available somehow. I now use another model, see information below. 

## model

The models below all read Chinese. it looks like the first one was only fine-tuned on simplified Chinese, whereas the second one was also fine-tuned on traditional Chinese. See https://www.sbert.net/docs/pretrained_models.html#multi-lingual-models and the corresponding Hugging Face pages for more information. 

We currently use: distiluse-base-multilingual-cased-v1.

alternative model: sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2 (appears to be the most popular, compare results). 

There are a few other models like ('shibing624/text2vec-base-chinese') that appear to have good performance, but I have trouble importing them.  


## converting the data
I found that the Fitz package appears to work well enough to convert most of the pdf to text. However, it is unable to read some of the scanned in documents on the first few pages of the PDF. I haven't tried to see if it works on all the pages with the pictures.

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
