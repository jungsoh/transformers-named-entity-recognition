# Transformer network: Named entity recognition

We explore an application of the transformer architecture by performing the following tasks:

* Use tokenizers and pre-trained models from the HuggingFace Library.
* Fine-tune a pre-trained transformer model for named entity recognition.

When faced with a large amount of unstructured text data, named entity recognition (NER) can help you detect and classify important information in your dataset. For instance, in the running example "Jane vists Africa in September", NER would help you detect "Jane", "Africa", and "September" as named entities and classify them as person, location, and time, respectively.

* We use the transformer model to process a large dataset of resumes.
* We find and classify relevant information such as the companies the applicant worked at, skills, type of degree, etc. 

## Dataset
Our dataset consists of a set of resumes represented in JSON format. 
```
	content	                                                annotation
0	Abhishek Jha Application Development Associate...	[{'label': ['Skills'], 'points': [{'start': 12...
1	Afreen Jamadar Active member of IIIT Committee...	[{'label': ['Email Address'], 'points': [{'sta...
2	Akhil Yadav Polemaina Hyderabad, Telangana - E...	[{'label': ['Skills'], 'points': [{'start': 37...
3	Alok Khandai Operational Analyst (SQL DBA) Eng...	[{'label': ['Skills'], 'points': [{'start': 80...
4	Ananya Chavan lecturer - oracle tutorials Mum...	[{'label': ['Degree'], 'points': [{'start': 20...
```
An annotation column is essentially a list of pairs of key and value representing the resume content, which may look like:
```
[{'label': ['Skills'],
  'points': [{'start': 1295,
    'end': 1621,
    'text': '\n• Programming language: C, C++, Java\n• Oracle PeopleSoft\n• Internet Of Things\n• Machine Learning\n• Database Management System\n• Computer Networks\n• Operating System worked on: Linux, Windows, Mac\n\nNon - Technical Skills\n\n• Honest and Hard-Working\n• Tolerant and Flexible to Different Situations\n• Polite and Calm\n• Team-Player'}]},
 {'label': ['Skills'],
  'points': [{'start': 993,
    'end': 1153,
    'text': 'C (Less than 1 year), Database (Less than 1 year), Database Management (Less than 1 year),\nDatabase Management System (Less than 1 year), Java (Less than 1 year)'}]},
 {'label': ['College Name'],
  'points': [{'start': 939, 'end': 956, 'text': 'Kendriya Vidyalaya'}]},
 {'label': ['College Name'],
  'points': [{'start': 883, 'end': 904, 'text': 'Woodbine modern school'}]},
 {'label': ['Graduation Year'],
  'points': [{'start': 856, 'end': 860, 'text': '2017\n'}]},
 {'label': ['College Name'],
  'points': [{'start': 771,
    'end': 813,
    'text': 'B.v.b college of engineering and technology'}]},
 {'label': ['Designation'],
  'points': [{'start': 727,
    'end': 769,
    'text': 'B.E in Information science and engineering\n'}]},
 {'label': ['Companies worked at'],
  'points': [{'start': 407, 'end': 415, 'text': 'Accenture'}]},
 {'label': ['Designation'],
  'points': [{'start': 372,
    'end': 404,
    'text': 'Application Development Associate'}]},
 {'label': ['Email Address'],
  'points': [{'start': 95,
    'end': 145,
    'text': 'Indeed: indeed.com/r/Abhishek-Jha/10e7a8cb732bc43a\n'}]},
 {'label': ['Location'],
  'points': [{'start': 60, 'end': 68, 'text': 'Bengaluru'}]},
 {'label': ['Companies worked at'],
  'points': [{'start': 49, 'end': 57, 'text': 'Accenture'}]},
 {'label': ['Designation'],
  'points': [{'start': 13,
    'end': 45,
    'text': 'Application Development Associate'}]},
 {'label': ['Name'],
  'points': [{'start': 0, 'end': 11, 'text': 'Abhishek Jha'}]}]
  ```
  
## Transformer model
We tokenize the input using the [🤗 DistilBERT fast tokenizer](https://huggingface.co/transformers/model_doc/distilbert.html) to match the DistilBERT transformer model we are using.
