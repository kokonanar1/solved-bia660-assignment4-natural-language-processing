Download Link: https://assignmentchef.com/product/solved-bia660-assignment4-natural-language-processing
<br>



Q1: Extract data using regular expression (

Suppose you have scraped the text shown belone from an online source. Define a <strong>extract</strong> function which:

takes a piece of text (in the format of shown below) as an input

extracts data into a list of tuples using regular expression, e.g. [(‘Grant Cornwell’, ‘College of

Wooster’, ‘2015’, ‘911,651’), …] returns the list of tuples

In [ ]: text=”’Following is total compensation for other presidents at privat e colleges in Ohio in 2015:

Grant Cornwell, College of Wooster (left in 2015): $911,651

Marvin Krislov, Oberlin College (left in 2016):  $829,913

Mark Roosevelt, Antioch College, (left in 2015): $507,672

Laurie Joyner, Wittenberg University (left in 2015): $463,504

Richard Giese, University of Mount Union (left in 2015): $453,800”’

<h1>Q2: Find duplicate questions by similarity (8 points)</h1>

A data file ‘quora_duplicate_question_500.csv’ has been provided as shown below. Each sample in this dataset has two questions, denoted as (<em>q</em><sub>1</sub>, <em>q</em><sub>2</sub>) (i.e.”q1″ and “q2” columns). Column “is_duplicate”=1 indicates if the two questions are indeed duplicate; otherwise, they are not duplicate, although they look similar. This dataset has 500 question pairs in total.

<strong>Q2.1.</strong> Define a function <strong>“tokenize”</strong> as follows:

takes three parameters:

<em>text</em>: input string.

<em>lemmatized</em>: an optional boolean parameter to indicate if tokens are lemmatized. The default value is False.

<em>no_stopword</em>: an optional bookean parameter to remove stop words. The default value is False.

splits the input text into unigrams and also clean up tokens as follows:

if <em>lemmatized</em> is turned on, lemmatize all unigrams.

if <em>no_stopword</em> is turned on, remove all stop words.

returns the list of unigrams after all the processing. (Hint: you can use spacy package for this task. For reference, check <u><a href="https://spacy.io/api/token#attributes">https://spac</a></u><a href="https://spacy.io/api/token#attributes">y</a><u><a href="https://spacy.io/api/token#attributes">.io/api/token#attributes </a></u><a href="https://spacy.io/api/token#attributes">(</a><u><a href="https://spacy.io/api/token#attributes">https://spac</a></u><a href="https://spacy.io/api/token#attributes">y</a><u><a href="https://spacy.io/api/token#attributes">.io/api/token#attributes)</a></u>)

<strong>Q2.2.</strong> Define a function <strong>get_similarity</strong> as follows:

takes the following inputs: two lists of strings (i.e. list of q1 and list of q2), and boolean parameters <em>lemmatized</em> and <em>no_stopword</em> as defined in (Q2.1). tokenize each question from the both lists using the “<strong>tokenize</strong>” function defined in (Q2.1). generates <strong>tf_idf matrix</strong> from the tokens obtained from the questions in both of the lists (hint:

reference to the tf_idf function defined in Section 8.5 in lecture notes. You need to concatenate q1 and q2)

calculates the <strong>cosine similarity</strong> of the question pair (<em>q</em><sub>1</sub>, <em>q</em><sub>2</sub>) in each sample using the tf_idf matrix returns similarity scores for the 500 question pairs

<strong>Q2.3.</strong> Define a function <strong>predict</strong> as follows:

takes three lists, i.e. list of similarity scores, “is_duplicate” column, and a <em>threshold</em> with default value of 0.5 as inputs if a similarity &gt; <em>threshold</em>, then predicts the question pair is duplicate calulates the percentage of duplicate questions pairs that are successfully identified, i.e. <em>co u n t</em> (<em>predictio n </em>= 1 &amp; <em>is</em>_<em>du plicate </em>= 1) <em>co u n t</em> (<em>is</em>_<em>du plicate </em>= 1)

returns the predicted values and the percentage

<strong>Q2.4. Test</strong>:

Test your solution using different options in in the tokenize function, i.e. with or without lemmatization, with or without removing stop words, to see how these options may affect the accuracy.

Analyze why some option works the best (or worst). Write your analysis in a pdf file.

<h1>Q3 (Bonus): More analysis</h1>

<strong>Q3.1</strong>. Define a function “<strong>evaluate</strong>” as follows:

takes three lists, i.e. list of similarity scores, “is_duplicate” column, and a <em>threshold</em> with default value of 0.5 as inputs if a similarity &gt; <em>threshold</em>, then predicts the question pair is duplicate, i.e. prediction = 1 calulates two metrics:

<em>recall</em>: the percentage of duplicate questions pairs that are correctly identified, i.e. <em>co u n t</em> (<em>predictio n </em>= 1 &amp; <em>is</em>_<em>du plicate </em>= 1) <em>co u n t</em> (<em>is</em>_<em>du plicate </em>= 1)

<em>precision</em>: the percentage of question pairs identified as duplicate are indeed duplicate, i.e. <em>co u n t</em> (<em>predictio n </em>= 1 &amp; <em>is</em>_<em>du plicate </em>= 1) <em>co u n t</em> (<em>predictio n </em>= 1)

returns the precision and recall

<strong>Q3.2</strong>. Analyze the following questions

If you change the similarity threhold from 0.1 to 0.9, how do precision and recall change? Consider both precision and recall, do you think what options (i.e. lemmatization, removing stop words, similarity threshold) can you give the best performance?

What kind of duplicates can be easily found? What kind of ones can be difficult to find? Do you think the TF-IDF approach is successful in finding duplicate questions?

These are open questions. Just show your analysis with necessary support from the dataset, and save your analysis in a pdf file.

In [ ]: <strong>if</strong> __name__ == “__main__”:




<em># Test Q1</em>




text=”’Following is total compensation for other presidents at pr ivate colleges in Ohio in 2015:

Grant Cornwell, College of Wooster (left in 2015): $911,651

Marvin Krislov, Oberlin College (left in 2016):  $829,913

Mark Roosevelt, Antioch College, (left in 2015): $507,672

Laurie Joyner, Wittenberg University (left in 2015): $463,504

Richard Giese, University of Mount Union (left in 2015): $453,800”’

print(“Test Q1”)     print(extract(text))

data=pd.read_csv(“../../dataset/quora_duplicate_question_500.csv”, header=0)

q1 = data[“q1”].values.tolist()     q2 = data[“q2”].values.tolist()




<em># Test Q2 </em>    print(“Test Q1”)

print(“<strong>
</strong>lemmatized: No, no_stopword: No”)     sim = get_similarity(q1,q2)

pred, recall=predict(sim, data[“is_duplicate”].values)     print(recall)




print(“<strong>
</strong>lemmatized: Yes, no_stopword: No”)     sim = get_similarity(q1,q2, <strong>True</strong>)

pred, recall=predict(sim, data[“is_duplicate”].values)     print(recall)




print(“<strong>
</strong>lemmatized: No, no_stopword: Yes”)     sim = get_similarity(q1,q2, <strong>False</strong>, <strong>True</strong>)

pred, recall=predict(sim, data[“is_duplicate”].values)     print(recall)




print(“<strong>
</strong>lemmatized: Yes, no_stopword: Yes”)     sim = get_similarity(q1,q2, <strong>True</strong>, <strong>True</strong>)

pred, recall=predict(sim, data[“is_duplicate”].values)     print(recall)




<em># Test Q3. Get similarity score, set threshold, and then </em>    prec, rec = evaluate(sim, data[“is_duplicate”].values, 0.5) Your output of Q2 may look like:

lemmatized: No, no_stopword: No 0.6304347826086957 lemmatized: Yes, no_stopword: No 0.782608695652174 lemmatized: No, no_stopword: Yes 0.6358695652173914 lemmatized: Yes, no_stopword: Yes 0.7717391304347826

<h1></h1>