# RNN

## Generated Text
ROMEO:
What, my weather's gainty, that? te-me toe?

Sicord,
And thou shallow shake her been cardon mercy and marriage,
And sad the hones of my duftless in that runsway faith he sidst
That the pity's heaven. I'll ten thou queen.

KING EDWARD IV:
Why, though Caius Marciusa-dear? then go this me and mank!

CAMILLO:
Speak it, well it: for I for our plots of levit?

IO GREMES:
What world I remain, my lords, will; I,
With his house of her very voices to thee it miserved
I'll go reach, I see that me in no shall dry.
I am plasted all, were I live; thou Dukes thy viphe
Wherein thy was of cary fortune I grievom's
Which that is rescended theme.

CORIOLANUS:
What to her henconce, farther Barns anagner
But now work at your heart,
Let a lord to Surrey times an exice,
We have no purity to eldurn.

ESCALUS:
Being arms?
Think easing Henry,' my Hastin suffer's dust:
My soul prove as the commends to Marcius.
Fear on't: but stand fortune, that
say as 'eforded too much of wil.

BRUTUS:
I have for my mestise: pas
## How it was Generated

This is a character-based model and before training the strings are converted into a numerical representation. preprocessing.StringLookup converts each character into a numeric ID and then tf.strings.reduce_join brings the characters back together into strings. 
After that preprocessing is complete, the training begins and the text was divided into example sequences and for each sequence the target will contain the same length of text, but shifted one character to the right using tf.data.Dataset.from_tensor_slices, then uses batch to convert characters into sequences of a specified size, and then strings are reformed. 
The training requires a dataset of (input, label), both input and label are sequences and are off by one character are mentioned above. After the data is split into sequences it is shuffled and put back into batches. 
The model that was built has three layers: Embedding, GRU, Dense. Embedding maps each character-ID to a vector, GRU is a type of RNN, and Dense is the output layer that outputs one logit for each character in the vocabulary. The model makes predictions about what the next character will be, indicated by a character's index previously defined, and then the predictions are decoded.
The model used SparseCategoricalCrossentropy as the loss function and uses adam as the optimizer. tf.keras.callbacks.ModelCheckpoint ensures that checkpoints are being saved during training. I ran this with 10 epochs and a batch size of 128. The model also uses a loop to generate text. The model has also learned when to capitalize and how to use the format of different characters speaking. 


