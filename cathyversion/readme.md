# readme
## Chapter 2 Results
Here are my results after modifying and running Ted's code from Chapter 2 in Distant Horizons. 

There is, in short, something funky going on: the differences in prediction results for individual texts are much more significant than expected, despite using the same data and code.

As an example, here are the different predictions for *Frankenstein*. Notice the swing, from a high of 63.68% to 2.98% (!!!). Ted does note that "you should not be surprised if you reproduce the modeling and get a result that is .1% - .5% higher or lower than the figure cited in the book," and while I'm not sure if that refers to the overall prediction accuracy for the body of texts (ie, 90%, see below) rather than the individual texts, these swings are still quite significant. 

*Frankenstein* results ('original' is from allSF.csv included in Ted's dataset)
|run|logistic|
|-|-----------|
|original|0.291827618| 
|run1|0.636840639| 
|run2|0.404216071| 
|run3|0.029794869| 
|run4|0.382415953| 
|run5|0.270088064| 
|run6|0.151365204|

This affected other titles as well, but to different degrees. I haven't measured the differences to see if an originally 98% title always stays high, for example.

|Run     |Frankenstein|L'an 2440  |From the Earth to the Moon|Neuromancer|Agrippa's Daughter|A Woman of the People|
|--------|------------|-----------|--------------------------|-----------|------------------|---------------------|
|original|0.291827618 |0.793768689|0.988856617               |0.660413425|0.259849582       |0.016881402          |
|1       |0.636840639 |0.991254586|0.999509278               |0.847632468|0.231697029       |0.009060675          |
|2       |0.404216071 |0.998690731|0.999999933               |0.948346372|0.1375839         |0.000222228          |
|3       |0.029794869 |0.981325119|0.999998929               |0.646468286|0.048015755       |0.000120089          |
|4       |0.382415953 |0.906242382|0.997495356               |0.832725942|0.196895609       |0.033855328          |
|5       |0.270088064 |0.992622757|0.999998804               |0.979639867|0.179094876       |0.002039043          |
|6		|0.151365204	|0.980802653185286|0.99944769095168|0.559788206462384|0.361590290782822|0.00152886269231822|

You can see the full spreadsheet in TrackSFModelling.csv, including the coefficents for the different runs.

Comparins Original data and Run 1:
![Original - labels](https://user-images.githubusercontent.com/12994156/183687565-7221e52e-8a87-4b29-93df-d4eb8b8be483.jpg)
![Run1 - labels](https://user-images.githubusercontent.com/12994156/183687651-2bab91df-e47a-4ebf-bdba-38882b5f72ea.jpg)



# My changes

These runs were done on either a Windows desktop (4 threads) or Windows Surface (2 threads), using an Anaconda/Python 3. 

I made minimal changes to the folder structure and Python files before running them:
 
1. Create lexicons folder in Ch2 (versatiletrainer.py needs to write to this folder)
	- this means that versatiletrainer.py is making its own lexicon; there is no comparison / original one included in the original repository
	- including the contents of the root/lexicon folder (MainDictionary.txt and so on) did not correct the variability
2. In versatiletrainer.py:
	- change the number of threads (based on computer power; 4 for my desktop, 2 for Surface)
	- comment out plt.show (for some reason, plt.show caused a hangup - I didn't experiment to see why)

When running the code, there aren't any flags.

# Here is an example of Run 6:

python reproduce.py allSF

Vocabulary for allSF already exists. Using it.

There are 1048 volumes described in metadata.
Of those, 1 were missing in the directory.
0 volumes in the directory were missing in metadata.
There were also 0 volumes excluded from the model by *excludeif*.

We have 213 positive, and 213 negative instances.

The whole corpus involved here includes 426 volumes, ranging in date from 1771 to 1999.

The set of volumes not to be trained on includes 0 positive volumes, ranging from 3000 to 0.

And also includes 0 negative volumes, ranging from 3000 to 0.

Number of features 6000
Training positives: 213
Training negatives: 213
426
compare
426
[22, 22, 22, 21, 21, 21, 21, 21, 21, 21]
[22, 21, 21, 22, 21, 21, 21, 22, 21, 21]

variablecount: 2000  regularization: 0.0003
Beginning multiprocessing.
Multiprocessing concluded.

Accuracy: 0.8732394366197183

variablecount: 2000  regularization: 0.001
Beginning multiprocessing.
Multiprocessing concluded.

Accuracy: 0.8873239436619719

[....and so on and so forth....]]


Final results
(8, 7)
2800 0.3
Beginning multiprocessing.
Multiprocessing concluded.

True positives 189
True negatives 196
False positives 17
False negatives 24
F1 : 0.9021479713603819
0.903755868544601 0.903755868544601
If we divide the dataset with a horizontal line at 0.5, accuracy is:  0.903755868544601


# Compare the above to Ted's results (as posted in labnotebook.md)

(21, 3) 
4100 0.006 
Beginning multiprocessing. 
Multiprocessing concluded.

True positives 186 
True negatives 200 
False positives 13 
False negatives 27 
F1 : 0.9029126213592233 
0.9061032863849765 0.906103286385 
If we divide the dataset with a horizontal line at 0.5, accuracy is: 0.906103286385

