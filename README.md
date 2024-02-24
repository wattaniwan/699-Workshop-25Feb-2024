## Workshop: 25 Feb. 2024 


### 1. Create Google Form with at least 5 questions.

### 2. Respond to the Google Form with at least 10 responses.

### 3. Find the sentiments of comments 

Add the Column "Sentiments" in to the response sheet.

Add a new sheet to track the number of responses and the number of assigned sentiments.

Create File **ass7-sentiment-xxx.ipynb** via Google Colab 

Modify the following example code for your work.


```
cd drive/MyDrive/!699-CaseStudySentiment

```


```
!pip install googletrans==4.0.0-rc1 textblob
!pip install gspread

```


```
# Authenticate and authorize access to Google Sheets
from google.colab import auth
auth.authenticate_user()

# Authorize with Google Sheets
import gspread
from oauth2client.client import GoogleCredentials
from google.auth import default

creds, _ = default()
gc = gspread.authorize(creds)

sheet = gc.open_by_key('1bJc6GaG9dAGIrOLem8N8fNtAvbSMqAJprUo4wnqb4uk')

worksheet1 = sheet.worksheet('Form Responses 1')
worksheet2 = sheet.worksheet('NumRespones')
```


```

#your defined function
from mysentimentxxx import translate_text,analyze_sentiment

#Get all values from the column 5,6
comments = worksheet1.col_values(5)
sentiments = worksheet1.col_values(6)

#Upate values
worksheet2.update_cell(2, 1, len(comments));  #numRes
worksheet2.update_cell(2, 2, len(sentiments)); #numSenti

n1 = len(sentiments)
n2 = len(comments)
for i in range(n1,n2):
  english_text = translate_text(comments[i])
  sentiment = analyze_sentiment(english_text)
  worksheet1.update_cell(i+1, 6, sentiment);
  print(comments[i],english_text, sentiment)
  

```


### 4. Visualize Data in the Response Sheet with Looker Studio 

Contain atleast 3 charts.

Must include the data about Sentiments

