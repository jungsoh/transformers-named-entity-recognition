# Transformer network: Named entity recognition

We explore an application of the transformer architecture by performing the following tasks:

* Use tokenizers and pre-trained models from the HuggingFace Library.
* Fine-tune a pre-trained transformer model for named entity recognition.

When faced with a large amount of unstructured text data, named entity recognition (NER) can help you detect and classify important information in your dataset. For instance, in the running example "Jane vists Africa in September", NER would help you detect "Jane", "Africa", and "September" as named entities and classify them as person, location, and time, respectively. 

* You will use the Transformer model to process a large dataset of resumes.
* You will find and classify relevant information such as the companies the applicant worked at, skills, type of degree, etc. 
