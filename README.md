# research-project


# Introduction
 Arabic is a Semitic language among the oldest in the world. The evolution of this language from antiquity to the present day has given birth to several linguistic registers; some forms have disappeared and others are still spoken. Four principle linguistic registers can be highlighted corresponding to the ancient Arabic language history.

- Old Arabic, which is not used currently and can be found in ancient literacy work
- Classical Arabic, which is the language of Islams Holy Book
- Modern Standard Arabic, the official language of all the Arab countries 
- Dialectal Arabic, which is the mother tongue of every Arabic speaker and used in daily life for spoken communication, changing from one Arab country to another.


A language will be called an under-resourced language if it has the following characteristics:  lack of a unique writing system or stable orthography, limited presence on the web, lack of linguistic expertise, lack of electronic resources for speech and language processing, vocabulary lists, etc. Dialects in general and Dialectal Arabic more specifically is an example of this category of languages since it is not standardized and does not usually have official status. Even though Modern standard Arabic is taught in schools and written conversations, most Arabic speakers are unable to produce sustained spontaneous speech in modern Standard Arabic in unscripted situations, it resorts to a mix between their dialect and standard Arabic. 

In Natural Language Processing (NLP) context, Standard Arabic has had its share of attention. Several sophisticated tools had been developed regarding the language but it has been proved not to be able to effectively model Arabic dialects. From this problem emerges the necessity to construct dedicated tools to process dialectal Arabic.
Working with dialects can have a huge positive impact on the standardization and preservation of their structure and identity. Voice activation algorithms using more complex language can also be a long-run perspective since using voice assistants has become ubiquitous with the popularity of Google Home, Amazon Echo, Siri, Cortana, and others.

*The objective of this project* is to produce a fairly effective speech recognition model on Tunisian dialect. The development of such a system faces the challenges of the lack of annotated resources and tools, apart from the lack of standardization at all linguistic levels (phonological, morphological, syntactic, and lexical). 
This project is therefore part of a research perspective to succeed in transferring low-density audio files to an adaptable language model.


# Toolkit and the project progress
## Data Resources

The main difficulty while working with under-resourced languages is the lack of
annotated resources and standardization at all linguistic levels. That is why choosing
carefully our data sets is a fundamental step in the process. 
For most under-resourced languages, there are no existing corpora that can be used for the development of ASR systems. Therefore, data collection is generally an integral part of ASR development in these languages. In order to train such models very large amounts of speech and textual data are generally required. 

### Annotated data

 The data set used in the project is from the Tunisian Arabic Railway Interaction Corpus (TARIC). The general architecture of a standard ASR system integrates three main components: acoustical (acoustic-phonetic) modeling, lexical modeling (pronunciation lexicon/vocabulary), and language modeling. Any state-of-the-art ASR system works in two modes: model training and speech decoding.

To develop ASR systems an amount of annotated resources is needed even if it’s limited.
The corpus used is gathered in collaboration with the Tunisian National Railway Company (SNCFT) and corresponds to recordings of information requests in railway stations. It was created to be used in similar projects and made open source.
This corpus, called TARIC (Tunisian Arabic Railway Interaction Corpus), contains information requests in the Tunisian dialect about the railway services such as train type, train schedule, train destination, train path, ticket price, and ticket booking. TARIC corpus is created in three stages: first, audio recording; second the orthographic transcription, and finally the transcription normalization. 

It contains more than 21k statements with a vocabulary of 3207 words for over 10 hours of audio data. 108 different speakers were recorded where 60 are males and 37 are females.
The data set came into separate audio files paired with a text document that contains the transcription and start and end time of each speech segment. 
### Unlabeled data 
For the unlabeled data, it was gathered from different Tunisian TV shows replays on YouTube. It was the most efficient way to get a good amount of data that can be used. Only the audio tracks were extracted and each file corresponded to the audio of a single episode of a specific Tunisian TV show. Over 450 hours of audio content was gathered to build the unlabeled database.
This corpus can be easily extended regarding the among of available clips on the internet. 

The difficulty with this unlabeled data is that it reacquires pretreatment since it contains a lot of noisiness and some music segments that can be confused with speech and influence our evaluation score on the training part. The challenge was to find a good Voice activity detection model that can isolate the speech segment and ignore music or random noise in the audio files.


## Virtual machine
A virtual machine was provided by OVHcloud to run the experiments since training neural networks reacquires strong Graphics processing units to speed up the computation when dealing with heavy data which is the case here. The virtual machine can also solve most of the libraries' importation technical issues.

## Steps for implementing an ASR model based on XLS-R and CTC

To build the ASR model on dialectal Arabic several architectures already exist and can be reused on the condition that it is fine-tuned on the unlabeled and labeled data presented previously.

The computation step are as follows :

-  Build a voice activity detection algorithm to prepare the unlabeled data set and extract only speech segments.
- Training XLS-R algorithm on the unlabeled data so it will learn the linguistic representation from the raw audio.
- Fine-tuning the model on the labeled data so it makes the link between the transcription of the words and the phonemes learned in the previous step. 

Many problems can be faced when working with annotated audio data since people’s rates of speech vary. This phenomenon can generate an alignment problem between the audio clip and the transcripted sentence. Connectionist Temporal Classification (CTC) is an algorithm that can be used as an extension of the main neural networks. This baseline aligns the audio to the text even if the audio section contains a different speed of speech which results in a better training
- Generate the sentences of a test data set and evaluate the model. 

Working on such problematic requires a good understanding of the theoretical bases of each pre-trained tool used in the process. It also can be time-consuming to work with audio data since it is considered a heavy format of files to load and manipulate. Still, despite having the major difficulty of limited data resources, we remain optimistic about the future scores of the training. 






For the bibliography, each fundamental step of the project had some interesting articles to deeply understand the theory behind the pre-trained model and be able to adapt it to the problem we are facing.\\

__Voice activity detection__

[1] Tom Bächstöm, Voice activity detection (VAD) - Introduction to Speech Processing,  Aalto University Wiki, 2019.

[2] H. Bredin, R. Yin, J. Manuel Coria, G. Gelly, P. Korshunov, M. Lavechin, D. Fustes, H. Titeux, W Bouaziz, M. Gill, Pyannote.audio: Neural building blocks for speaker diarization, 2019.1111.


[3] A. Graves, N. Jaitly and A. Mohamed, Hybrid Speech Recognition With Deep Bidirectional LSTM, University of Toronto, 2013.

[4] G. Gelly and J. Gauvain, Optimization of RNN-Based Speech Activity Detection, 2018.

__Connectionist Temporal Classification :__

[5]  Harald Scheidl, "An Intuitive Explanation of Connectionist Temporal Classification", TDS, 2018.

[6]  Hannun, "Sequence Modeling with CTC", Distill, 2017.

[7]  A. Masmoudi, F. Bougares, M. Ellouze, Y. Esteve, L. Belguith, "Automatic Speech Recognition System for TunisianDialect", Language Resources and Evaluation, Springer Verlag, 2018.


[8] X. Kong, J. Choi, S.Shattuck Hufnagel, "Evaluating Automatic Speech Recognition Systems in Comparison With Human Perception Results Using Distinctive Feature Measures", IEEE, 2017.


[9]  Mirco Ravanelli and Titouan, "Introduction to SpeechBrain", SpeechBrain official site, 2021.

__XLS-R__ 

[10] A. Baevski, H. Zhou, A. Mohamed, M.l Auli, wav2vec 2.0: A Framework for Self-Supervised Learning of Speech Representations,2020.


[11] P. von Platen, Fine-Tune XLSR-Wav2Vec2 for low-resource ASR with Transformers, 2021.


[12] XLS-R: Self-supervised speech processing for 128 languages by Meta IA 2018.

