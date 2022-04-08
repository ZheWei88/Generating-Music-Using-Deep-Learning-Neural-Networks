# Introduction

**<i>"Twelve notes and the octave repeats. It's the same story told over and over, forever. All any artist can offer the world is how they see those twelve notes. That's it."</i>**
<br>
\- Sam Elliott as Bobby - A Star Is Born (2018)

Yes, indeed there are only 12 notes - **A, Bb, B, C, Db, D, Eb, E, F, Gb, G, Ab** - and the cycle repeats.

With such few notes available to musicians, is no wonder we are sometimes stuck in a creative rut, unable to come up with a good melodies.


# Problem Statement
It can be difficult at times for musicians to come up with melodies and their accompanying chords. This can often lead to undue frustrations and stress on the musician, producer and record labels, as well as incurring monetary costs due to the additional time spent in the recording studio or delays in song releases.<br>
In view of this, I plan to develop and model that can generate melodies and their accompanying chord progressions with a random or manual input.
With this model that is able to generate it's own music, I hope to save costs in the music industry by reducing the time taken to write catchy songs.

# The Music Data

## Train set
The data from the train set is obtained from https://github.com/Skuldur/Classical-Piano-Composer. As such, the model and findings from this project are the progression from this earlier project.

The songs in this dataset consists mostly of classical pieces from Japanese Role Playing Games (JRPGs) such as Final Fantasy.

## Test set
The data from the test set is obtained from Kaggle from programgeek01/anime-music-midi, and consists mainly of classical songs from popular Japanese animes such as 'Demon Slayer' and 'Attack on Titan'. This dataset was chosen as it is of the similar genre to the train dataset.

## EDA on the datasets

||Train Dataset|Test Dataset|
|---|---|---|
|No.of songs|92|130|
|No. of elements|62,367|97,424|
|Average song length|677.9|749.42|
|Unique notes/chords|382|437|
|Unique durations|173|70|

The test data is greater than the train data in all areas except the 'Unique Durations', where the train set has more durations than the test set.

# Preprocessing
1. Separate the notes/chords and durations of individual songs.
    - As choice of notes/chords and durations usually have little influence on each other we will train them separately.
2. Map each note/chord and duration(key) to an integer(value).
    - {'C4':0,'C5':1…}, {'0.25':0,'0.5':1…}
3. Add unknown variable as ‘unkw’ to the integer value of 0.
    - This will allow model to process elements present in test data, but not present in train data.
    - {'unkw':0,'C4':1…}, {'unkw':0,'0.25':1…}
4. Convert the notes/chords and durations sequences into integers.
5. Prepare data to fit to model
    - Input
        - Divide into lists of 100 elements each, where each new list contains the 1st - 101st element relative to previous list.
        1. [0,1,2…100]
        2. [1,2,3…101]
        ...

    - Output
        - Each output will be the 101st element of the 100 note input
        1. [101]
        2. [102]
        ...

# Model
The model has 3 main components:
1. Embeddings layer
    - By passing the input through an Embedding layer, the model can learn which notes/chords or durations are closely related to each other, which will ultimately help with predictions.
2. Bidirectional LSTMs
    - Used to process entire sequences of music data without treating each point in the sequence independently, but rather, retaining useful information about previous data in the sequence to help with the processing of new data points.
3. Dense layers
    - Regular dense layers which include Acivation Funcations like ReLU and Softmax.

**Notes/chords and durations are separated, and will be trained separately using the same model architecture.**

## Training Process
We use accuracy as a guide to the progress of the model.
1. 50% - https://soundcloud.com/zhe-wei-3/50a?utm_source=clipboard&utm_medium=text&utm_campaign=social_sharing
2. 80% - https://soundcloud.com/zhe-wei-3/80a?utm_source=clipboard&utm_medium=text&utm_campaign=social_sharing
3. 90% - https://soundcloud.com/zhe-wei-3/90a?utm_source=clipboard&utm_medium=text&utm_campaign=social_sharing
4. 97% - https://soundcloud.com/zhe-wei-3/97a?utm_source=clipboard&utm_medium=text&utm_campaign=social_sharing

## Model Insights
Now that we have proven that this model is capable of generating it's own music, we want to investigate if it is capable of learning some 'music theory'.

We can do so by applying cosine similarity to the 'Embeddings' layer of the model.

For note **A2**

||Cosine Similarity|
|---|---|
|'A', 'B', 'C#'|0.400902|
|'G', 'Bb', 'C#', 'Eb'|0.39942|
|'B'|0.369358|

'A', 'B', 'C#' make up the Aadd(2) chord, which is a variation of the A chord. Furthermore, all 3 notes are in the key of A major.


'G', 'Bb', 'C#', 'Eb' make up the Eb7/G. This combination of notes is rarely seen in western music, but is more common in eastern music, and is a likely blend of the D harmonic minor and A harmonic minor, both of which feature the A note.


'B' is a prominent note in both the key of A major and A minor.

It would appear that the model did in fact learn some music theory!

# Conclusions and Recommendations
As can be seen, or rather, heard, from the music generated, neural networks are quite capable of generating their own music. The music generated using the best model (highest accuracy and lowest loss), sounds pleasing and contains a few good musical ideas.

While not a complete replacement of the human musician, such generated music can no doubt assist the human musician in compositions, which is one of the key objectives of this project.

A further investigation on the embeddings layer in the model has shown that the model is even capable of understanding music theory, which, given a larger dataset, will definitely be able to generate music of greater length and musicality.

That said, there are a number of improvements that can be made to this model, which can be explored with future iterations of this project:
1. The songs are still of one part, and it would be great to have multiple parts fed into the model. The limitation of the LSTM is that the input has to be one dimensional. There is  a way to input more than one dimension to the LSTM, which is highlighted here https://keras.io/guides/functional_api/. If more instruments can be added, it will add a greater degree of complexity and dynamics to the generated music.<br>


2. Only piano music is used for the model. The reason is that piano music is the least dynamic, with most notes being staccato, where each note sharply detached or separated from the others. To incorporate legato, where notes are played in a smooth flowing manner, without breaks between notes, or other techniques used on other instruments such as guitar or violin, would require another dimension of input, which would make the case for multiple degree input mentioned in point 1, to the LSTM even stronger.<br>


3. LSTMs are increasingly being replaced by transformers. So adapting the model in this project to incoporate transformers rather than LSTMs would be something to explore in the future.<br>


4. One of the other goals of this project was to generate a melody from a chord progression. While I ultimately did not do this, it is something that can be pursued in the near future, as models such as seq2seq architecture, which is widely used in translations, can potentially fufil this task, with the input 'language' being the chord progression, and with the output 'language' being the melody.
