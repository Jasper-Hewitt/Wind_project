# Wind_project

it appears to work: see finding_noisepollution. 

## todo
- figure out what that warning is: cannot find model with this name... Maybe it's not really using the model now. Otherwise check for other models.
- read and highlight the actual pdf and see if the model gets it right
- count the total number of words after converting and check how many was lost.
- check why the len of sentence_score is only half of that of split_contents. Maybe I'm losing a lot of sentences here. 

This is the main one: https://github.com/Jasper-Hewitt/Wind_project/blob/main/similarity_shibing624.ipynb. It appears to be working pretty well

There's also one that uses distilbert: but it doesn't show a score. 

it also works with entire paragraphs. However it makes one crucial mistake because it assigns 0.000 overall similarity score to a sentence that contains all the keywords. Maybe this is just because of a mistake in teh calculation part. Have to verify that

code is based on: https://www.sbert.net/examples/applications/semantic-search/README.html




For semantic research using open AI API, see: 
see also: https://www.youtube.com/watch?v=ocxq84ocYi0 
