# l14-crypt
Message encoder/decoder with a few transposition cipher methods.

## Available ciphers

### Reverse or r
As the name suggests, return reversed plaintext;

eg: Hello world = dlrowolleH

### Caesar's or c
This cipher was used by the Roman emperor Julius Caesar, thus the name. It is a type of substitution cipher in which each letter in the plaintext is replaced by a letter some fixed number of positions down the alphabet, used with --shift or -s to define it. [More info](https://en.wikipedia.org/wiki/Caesar_cipher);

eg: Hello world = Khoorzruog
Default shift used, which is 3

### Character to number or n
Replaces each letter with it's position index on the alphabet.

eg: Hello world = 8 5 12 12 15 23 15 18 12 4
A = 1, B = 2, C = 3 ... 

### Horizontal matrix or h
Aka [columnar transposition](https://en.wikipedia.org/wiki/Transposition_cipher#Columnar_transposition). Use --horizontal_shift or -hs to define column size;

eg: Hello world = Holewdlolr
Default horizontal shift used, which is 4.

### Alternate first as second or a
Simple replace first with second, third with fourth and so on;  

eg: Hello world = eHllo owlrd

### Random transposition key or rk
Rearrange the plaintext randomly, and generating a key with the original position indexes for decryption;  

eg: Hello world = dlHwrlleo o
Generated key: 10 9 0 6 8 2 3 1 7 5 4


## Possible arguments

### --help or -h
No surprises, it displays help message and usage;

### --shift or -s
Use with Caesar's method to define how long to jump, default is three;

### --horizontal_shift or -hs
Same as shift, but to define column size of the horizontal matrix, default is four;

### --preserve_whitespaces or -pw
Use it to preserve whitespaces. Keep in mind that this may alter the result with a few methods, thus being need to be passed as argument when decrypting, default is false;

### --key or -k
Specify the key to decrypt messages in key-based decryption;

### --output or -o
Saves it to a external file. The first argument is for location, the other one to the method (w)rite or (a)ppend;

### --input or -i
Open an external file and use it as message, simply type the location of the file;

### --clear or -c
Tries to clear screen before showing ciphered message, default is true;

### --copy or -co
Tries to copy the ciphered message to clipboard, using clip on windows, pbcopy on mac, and xsel to clipboard or xclip in linux based systems. Default is false;

## Use examples

python3 main.py "just testing" e a r  
Output: ginsttestju
My message here is just testing, I want to (e)ncrypt using (a)lternate method and (r)everse;

./main.py "ginsttestju" d reverse Alternate  
Output: justtesting
I'm on a unix system like and have given exec permissions to my main.py script, passed the previous output as input message for (d)ecrypt using (r)everse, and (a)lternate methods. You get the idea, right? Since I've encrypted using alternate and then reverse, I first need to reverse and then alternate to get to the original message. White spaces weren't preserved, thus the words are stuck together.

./main.py "Hello World" e c -s 10 -pw  
Output: Rovvy Gybvn

./main.py "Hello World" e h --horizontal_shift 2 -pw --copy  
Output: HloWrdel ol  
Sucessfully copied to clipboard

./main.py "lHoold rWle" d rk -k 9 0 4 7 3 10 5 8 6 2 1 --preserve_whitespaces -o ./my_output.txt w  
Output: Hello World 

./main.py --input ./my_output.txt e reverse  
Output: dlroWolleH 