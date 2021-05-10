# tf-transliteration-riggs2slo-toolkit
This app is built with help from the source code provided by Kolloldas here: https://github.com/kolloldas/tf-transliteration

Work on this app was performed to assist the Wóoyake Project in transliterating documents from Riggs orthography as used in news articles such as Iape Oaye. The model currently contained in this app is version **1.9** and has been trained on 27 documents consisting of 11000 word pairs.

# Prerequisites
This software was designed to be run easily on Microsoft Windows, and has been tested on Windows 10 Pro with 4 GB of RAM and no dedicated graphics card.

You will need:

* Python 3.5
* Tensorflow 1.5
* Visual C++ 2015 Redistributables Update 3 (for Python 3.5, which can be found here: [Link](https://www.microsoft.com/en-us/download/details.aspx?id=53587))
* Java

If you are an advanced user, you can simply use the app directly in the tf-transliteration folder. You can do this by using the same instructions indicated on the tf-transliteration project by Kolloldas: [Link](https://github.com/kolloldas/tf-transliteration). This may be necessary (and easier) when running transliteration on Linux or Mac operating systems.

# Installation Instructions
Having the repository downloaded with the prerequisites installed on your computer is enough to begin transliterating. If you have done so already, you can skip to How to Use. The following will describe how to install the above prerequisites.

## Installing Python 3.5
You can find Python 3.5.4 from the following link:

https://www.python.org/downloads/release/python-354/

Install the version that is appropriate for your version of Windows. Ensure that the version of Python that you install is installed for "all users".

To verify that Python is installed properly, open **Command Prompt** by click Start > type "Command Prompt" and open the first result. Then type the following command: `Python -V` and hit Enter. You should see "Python 3.5.4" appear.

If anything else happens, such as the Microsoft Store opening, your Command Prompt can't find Python. Either it wasn't installed properly, or Command Prompt was open while Python was installing. Simply close and reopen Command Prompt and try the command again in that case.

We cannot ensure compatibility with another Python version newer than 3.5.4 that isn't also compatible with Tensorflow 1.5. If you install a different version of Python, you do so at your own risk.

## Installing Tensorflow 1.5
You need a compatible Python installed to install Tensorflow 1.5. If you installed Python 3.5.4, then your Python can install Tensorflow 1.5.

To install Tensorflow, open the **Command Prompt** by clicking Start > type "Command Prompt" and open the first result. Then type the following command: 

`python -m pip install tensorflow=="1.5"`

And hit enter. Let the installation complete in the Command Prompt window. 

If the installation doesn't begin, you may need to open the Command Prompt as Administrator. To do this, find Command Prompt as above, then right click on the Command Prompt icon, and click on "Run as Administrator".

Tensorflow 1.5 should be installed, but will not run without Visual C++ 2015 Redistributables Update 3, which can be found and installed here: https://www.microsoft.com/en-us/download/details.aspx?id=53587

## Installing Java
To install Java, download the Java installer from the official Java website here: https://www.java.com/en/
Then simply open the installer and follow the onscreen instructions.

# How to Use
Once you have ensured all the prerequisite installations are complete, you are ready to use the app.

Place the files you want to transliterate in the input folder. Only .txt files in the input folder will be transliterated. To support non-ASCII characters, ensure the .txt files are encoded in UTF-8.

When run-transliteration.bat is run, the files in the input folder are enumerated, and their type is determined based on what it finds inside each file:

* If there is no punctuation found that generally delimits sentences or phrases, such as periods or question marks, then the txt file is processed in **word mode.**
* If there is such punctuation found, then the txt file is processed in **paragraph mode.**

How these files are processed is described below:

## Word Mode
In word mode, each newline delimits a unique word. Each word is transliterated using the included model. The output folder will contain the transliterated word in a .txt format in the same order that was taken in. 

Please note that any whitespace, such as spaces or tabs, are not visible to transliteration and words separated by whitespace will be joined together.

This is the simplest format for transliterating a batch of words.

## Paragraph Mode
Paragraph mode is optimized for transliterating documents that depict full sentences rather than singular words.

In paragraph mode, the text is split by newlines, then by whitespace to isolate groups of characters as words. Any non-alphanumeric text in these words are tokenized and removed from the word content. Any word that has a trailing hyphen will be combined with the next word with the hyphen removed, as if they were broken by newline. 

The resulting text is then transliterated, treated as a word list. Finally, the transliterated text is paired back with its tokens and the lost text content is regenerated using the information stored in each token.

The output folder will contain a .txt with each sentence placed on a new line.

This option doesn't perfectly preserve the formatting of the original input text, but it performs a lot of work to retain the formatting of the original input text.

# Model Accuracy
This model does not discern context within a given sentence or paragraph in relation to meaning or other words. As such, when transliterating from Riggs to SLO, you should be aware of what the original word may have been in Riggs and determine if the word produced in SLO is a valid Dakota/Lakota word or phrase. 

The primary goal of this tool is to accelerate the workflows required in transliterating documents written in Riggs orthography. It will both assist individuals who have no intimate knowledge of the Dakota/Lakota language and accelerate workflows for individuals who do. Hence, we are always looking to improve the accuracy of the model, and may periodically provide updated versions of the model that make less mistakes.

# Updating the Model
If we release a new model, you can replace the contents of the tf-transliteration folder with that of a tf-transliteration folder associated with a newer model. The app should be capable of using any model that is placed there and use it to transliterate your text.

The current model version is **1.9**.
