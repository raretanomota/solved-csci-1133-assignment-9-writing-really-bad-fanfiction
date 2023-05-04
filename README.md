Download Link: https://assignmentchef.com/product/solved-csci-1133-assignment-9-writing-really-bad-fanfiction
<br>
<h1></h1>

Getting computers to produce convincing English sentences about a particular topic is a challenging problem, so we won’t be doing that in this assignment.  Instead, we’ll use a shortcut that quickly produces nonsense that somewhat resembles coherent English.  Given a sequence of sentences on a topic (for example, a novel), our strategy to produce a sentence will be as follows:

<ul>

 <li>For each distinct word in the novel, determine how frequently any other given word follows it, including how frequently nothing follows it (because the sentence ends). Note that capitalization matters here: we are counting ‘Hello’ and ‘hello’ as distinct words (this will help ensure that our sentences usually start with capitalized words).</li>

 <li>To start generating a sentence, pick a word at random from any of the words that start a sentence in the novel.</li>

 <li>To generate the next word, pick one of the words that followed the current one at random (in a weighted format, so if word A is followed by word B twice as often as word C in the novel, then word A is twice as likely to be followed by word B than word C in our sentence). This includes the possibility of picking nothing.</li>

 <li>Keep choosing words until nothing is picked, at which point the sentence ends.</li>

</ul>




To do this, you need to write three functions (the first two are helper functions for the last one).  Be sure you match the names and parameters of the functions exactly to prevent grading issues.




first_words(fname) takes in fname, a string representing the name of a file, and returns a list of the first word in every sentence in that file, in order, including duplicates.  See below for specifications on the formatting of the input file.  You can assume that the file specified actually exists (i.e. you don’t have to worry about handling FileNotFoundError on this problem).




next_words(fname) takes in fname, a string representing the name of a file, and returns a dictionary where the keys are each distinct word in the file (case matters), and the value for any given key is a list of every word that follows that key anywhere in the file, in order, including duplicates.  In the case that a given key appears as the last word of a sentence, you should add the string “.” to the list instead of the word that follows it.




fanfic(fname) takes in fname, a string representing the name of a file, and prints 10 ‘sentences’, one per line, based on that file, as described above.  In particular, the first word of the sentence should be randomly chosen from the list produced by first_words (use random.choice, which chooses an element at random from a list).  Each word produced should then be used as a key into the dictionary produced by next_words, and then the next word should be chosen at random from the list that is the value for that key.  The sentence should end when “.” is chosen.  The function should not return anything.




You can make the following assumptions about the input files (see the examples provided on Canvas):

<ul>

 <li>They exist in the directory the script is being run from, and are readable text files.</li>

 <li>Every line will be a single sentence, ending with a period (separated from the last word by a space). Each word in a given sentence will be separated by a single space.</li>

 <li>There will be no other punctuation in the file, aside from apostrophes used in contractions.</li>

</ul>




<strong>Constraints</strong>:

<ul>

 <li>Do not import/use any Python modules other than random</li>

 <li>You may use any string or list method that is appropriate to solving this problem.</li>

 <li>Don’t use the input() function, as this will break our grading scripts.</li>

 <li>Your submission should have no code outside of the function definitions, aside from comments and import random.</li>

</ul>




<strong>Examples </strong>(download the sample text files from Canvas into the folder you’re running hw9.py from):

&gt;&gt;&gt; first_words(‘short1.txt’)

[‘Never’, ‘Never’, ‘Never’]




&gt;&gt;&gt; first_words(‘short2.txt’)

[‘Fear’, ‘Fear’, ‘Anger’, ‘Hate’, ‘I’]




(note: remember that order does not matter for dictionaries, so you may get the keys in a different order in the next two examples, but the key-value pairings should be the same)




&gt;&gt;&gt; next_words(‘short1.txt’)

{‘let’: [‘you’], ‘down’: [‘.’], ‘Never’: [‘gonna’, ‘gonna’, ‘gonna’],

‘gonna’: [‘give’, ‘let’, ‘run’], ‘and’: [‘desert’], ‘up’: [‘.’],

‘run’: [‘around’], ‘you’: [‘up’, ‘down’, ‘.’], ‘around’: [‘and’],

‘give’: [‘you’], ‘desert’: [‘you’]}




&gt;&gt;&gt; next_words(‘short2.txt’)

{‘anger’: [‘.’], ‘dark’: [‘side’], ‘I’: [‘sense’], ‘the’: [‘path’, ‘dark’], ‘you’: [‘.’], ‘Anger’: [‘leads’], ‘much’: [‘fear’], ‘Hate’:

[‘leads’], ‘fear’: [‘in’], ‘sense’: [‘much’], ‘to’: [‘the’, ‘anger’,

‘hate’, ‘suffering’], ‘side’: [‘.’], ‘leads’: [‘to’, ‘to’, ‘to’],

‘Fear’: [‘is’, ‘leads’], ‘path’: [‘to’], ‘is’: [‘the’], ‘hate’: [‘.’],

‘in’: [‘you’], ‘suffering’: [‘.’]}




(note: the output of fanfic is random, so these test cases only demonstrate the format of the output:

your actual sentences will not match)




&gt;&gt;&gt; fanfic(‘alice_in_wonderland.txt’)

I only been the Hatter .

Keep back by the best .

Come away .

While the second thing she crossed her head pressing against the Hatter and looking party went on half shut his eyes then said Alice thought .

The Hatter continued in despair she felt quite a vegetable . If you see it really you are the Caterpillar and get through that he began in livery came very like an air .

Then I’ll write this be no use of the question but she put on just as the simple question said the air Do you begin lessons you’d better leave out to the right said Alice who is .

First because they’re only as they don’t fit .

The Duchess she waited to herself and after the fan and the other guests mostly Kings and very slowly back by the White Rabbit Hole . So Bill’s got altered .




&gt;&gt;&gt; fanfic(‘wizard_of_oz.txt’)

So he had they were waiting in a slate from the room .

She sprang into the most noble Sorceress to Kansas again I know it gently on he was .

Dorothy said and sharp edge of the Woodman’s weapon .

So they fluttered in a great sorrow was to the silk into her .

The Lion she was frightened when the daylight the other in the Tin

Woodman to forgive us answered the green . These tears of the Scarecrow .

We must run away through the Scarecrow twisted its body was so brightly in the huge beast .

I got the King of towers and you not know what made of the magic words the animals as he wishes .

The fences and as I may thereafter be dreadfully worried Dorothy heard a plate to help to guard against mishap .

They now came to fool me back so she asked Is he said to an instant the china fences at him a heart beat fast asleep .




<h1>Problem B. (20<em> points</em>)  Directory Traversal</h1>

One method for representing a simple file system is with nested dictionaries, where each dictionary represents a directory.  Each key represents the name of either a file or a subdirectory, and each value is either another dictionary for a subdirectory, or metadata for a file.  In this case, we’ll be looking at memory usage, so the value for each file key will be the size of the file in bytes.  For example, we could represent the directory root in the image below as the following dictionary:




root = {‘labs’:{‘lab1.txt’:223,                 ‘lab2.txt’:251,

‘lab3.txt’:317,},

‘hws’:{},

‘plans’:{‘vacation.txt’:636,

‘evil’:{‘world_domination.txt’:766}},

‘resume.txt’:607,

‘cat.jpg’:607}










Write a function total_txt_size(directory) that takes in a nested dictionary representing a directory as explained above, and returns the total memory in bytes (an integer) being used by txt files in the directory (that is, any file where the last four characters in the filename are ‘.txt’).




<strong>Hints: </strong>

<ul>

 <li>You need to sum the memory of all .txt files within the directory at any level within the hierarchy, so this includes files in the root directory, files in subdirectories of the root, files in subdirectories of those subdirectories, and so on.</li>

 <li>You’re not required to use recursion, but it will probably make the solution much simpler. This is an example of tree traversal, a problem type that is particularly suited to recursive solutions.</li>

 <li>To check whether a given element in the dictionary represents a file or a subdirectory, check whether the value in the key-value pair is type int.</li>

</ul>




<strong>Constraints</strong>:

<ul>

 <li>Do not import/use any Python modules (except random for part A)</li>

 <li>Don’t use the input() function, as this will break our grading scripts.</li>

 <li>You may use any string or list method that is appropriate to solving this problem.</li>

 <li>Your submission should have no code outside of the function definitions, aside from comments and import random.</li>

</ul>




<strong>Examples</strong>:

&gt;&gt;&gt; root1 = {‘time_travel’:{‘micro_black_holes.zip’:100,

‘quantum_realm.pdf’:150,

‘magic.txt’:200},

‘space_travel’:{‘tesseract.java’:400,

‘magic.txt’:100,

‘warp_drive.py’:300,

‘mass_relay.txt’:100}}

&gt;&gt;&gt; total_txt_size(root1)

400




&gt;&gt;&gt; root2 = {}

&gt;&gt;&gt; total_txt_size(root2)

0




&gt;&gt;&gt; root3 = {‘labs’:{‘lab1.txt’:223,

‘lab2.txt’:251,

‘lab3.txt’:317,},

‘hws’:{},

‘plans’:{‘vacation.txt’:636,

‘evil’:{‘world_domination.txt’:766}},

‘resume.txt’:607,

‘cat.jpg’:607}

&gt;&gt;&gt; total_txt_size(root3)

2800




&gt;&gt;&gt; root4 = {‘a’:{‘b’:{‘c’:{‘d’:{‘e’:{‘f.c’:10}},’g.txt’:12}}}}

&gt;&gt;&gt; total_txt_size(root4)

12


