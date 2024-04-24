PREM.R
 212223240124
<H3>EX. NO.6</H3>
<H3>DATE:</H3> 24/02/24
<H1 ALIGN =CENTER>Implementation of Semantic ANalysis</H1>
<H3>Aim: to perform Parts of speech identification and Synonym using Natural Language Processing (NLP) techniques. </H3> 
 <BR>
<h3>Algorithm:</h3>
Step 1: Import the nltk library.<br>
Step 2: Download the 'punkt', 'wordnet', and 'averaged_perceptron_tagger' resources.<br>
Step 3:Accept user input for the text.<br>
Step 4:Tokenize the input text into words using the word_tokenize function.<br>
Step 5:Iterate through each word in the tokenized text.<br>
•	Perform part-of-speech tagging on the tokenized words using nltk.pos_tag.<br>
•	Print each word along with its corresponding part-of-speech tag.<br>
•	For each verb , iterate through its synsets (sets of synonyms) using wordnet.synsets(word).<br>
•	Extract synonyms and antonyms using lemma.name() and lemma.antonyms()[0].name() respectively.<br>
•	Print the unique sets of synonyms and antonyms.
<H3>Program:</H3>
```
import nltk
from nltk.corpus import wordnet
import csv
nltk.download('averaged_perceptron_tagger')
nltk.download('wordnet')
nltk.download('punkt')


def get_verbs(sentence):
    verbs = []
    pos_tags = nltk.pos_tag(nltk.word_tokenize(sentence))
    for word, tag in pos_tags:
        if tag.startswith('V'):  # Verbs start with 'V' in the POS tag
            verbs.append(word)
    return verbs


def get_synonyms(word):
    synonyms = []
    for syn in wordnet.synsets(word):
        for lemma in syn.lemmas():
            synonyms.append(lemma.name())
    return synonyms


def read_text_file(file_path):
    with open(file_path, 'r') as file:
        text = file.read()
    return text

def main():
    file_path = 'sample.txt'

    text = read_text_file(file_path)
    sentences = nltk.sent_tokenize(text)

    all_verbs = []
    synonyms_dict = {}

    for sentence in sentences:
        verbs = get_verbs(sentence)
        all_verbs.extend(verbs)
        for verb in verbs:
            synonyms = get_synonyms(verb)
            synonyms_dict[verb] = synonyms

    with open('output.csv', 'w', newline='') as csvfile:
        writer = csv.writer(csvfile)
        writer.writerow(['Verb', 'Synonyms'])
        for verb, synonyms in synonyms_dict.items():
            writer.writerow([verb, ', '.join(synonyms)])


if __name__ == '__main__':
    main()
 ```




OUTPUT:
![Screenshot 2024-04-24 081822](https://github.com/PREM3112/Ex-6--AAI/assets/145449383/67db9e0b-a0e6-4ec8-8eca-c15eea9c09da)






<H3>Result:</H3>
Thus ,the program to perform the Parts of Speech identification and Synonymis executed sucessfully.
