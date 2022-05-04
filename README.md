
#  Decoder ring
This project is designed to test my ability to build tricky algorithms as well as write unit tests with Mocha and Chai. I built functions for an application that will either encode or decode a string using a variety of ciphers. For each cipher, I have made a series of tests using Mocha and Chai to confirm that the cipher works.

All of the functions can be found inside of the src/ directory. Each function and cipher is described below.

## Caesar shift
![Caesar Shift](https://res.cloudinary.com/strive/image/upload/w_1000,h_1000,c_limit/7a945612b738d811880b0244ee5ec0a2-image.png)

The Caesar shift is a type of substitution cipher originally used by Julius Caesar to protect messages of military significance. It relies on taking the alphabet and "shifting" letters to the right or left, based on the typical alphabetic order.


For example, if you were to "shift" the alphabet to the right by 3, the letter A would become D.

    caesar(input, shift, encode = true)
    "thinkful" -> "wklqnixo"

The `caesar()` function in the src/caesar.js file has three parameters:

`input` refers to the inputted text to be encoded or decoded.  
`shift` refers to how much each letter is "shifted" by. A positive number means shifting to the right (i.e., A becomes D) whereas a negative number means shifting to the left (i.e., M becomes K).  
`encode` refers to whether you should encode or decode the message. By default it is set to `true`.
When building the function, keep the following constraints and rules in mind:  

Examples

    caesar("thinkful", 3); //> 'wklqnixo'
    caesar("thinkful", -3); //> 'qefkhcri'
    caesar("wklqnixo", 3, false); //> 'thinkful'
    
    caesar("This is a secret message!", 8); //> 'bpqa qa i amkzmb umaaiom!'
    caesar("BPQA qa I amkzmb umaaiom!", 8, false); //> 'this is a secret message!'
    
    caesar("thinkful"); //> false
    caesar("thinkful", 99); //> false
    caesar("thinkful", -26); //> false

## Polybius square
| |1|2	|3|	4|	5|
|--|--|--|--|--|--|
|1|	A|	B|	C|	D|	E|
|2|	F|	G|	H|	I/J|K|
|3|	L|	M|	N|	O|	P|
|4|	Q|	R|	S|	T|	U|
|5|	V|	W|	X|	Y|	Z|

The Polybius square is a cipher that is achieved by arranging a typical alphabet into a grid. Each letter is represented through a coordinate. For example, in the above table, the letter B would be represented by the numerical pair 21.

     polybius(input,encode=true)
    "thinkful" -> "4432423352125413"

The `polybius()` function in the src/polybius.js file has two parameters:

`input` refers to the inputted text to be encoded or decoded.
`encode` refers to whether you should encode or decode the message. By default it is set to true.

Examples

    polybius("thinkful"); //> "4432423352125413"
    polybius("Hello world"); //> '3251131343 2543241341'
    polybius("3251131343 2543241341", false); //> "hello world"
    polybius("4432423352125413", false); //> "th(i/j)nkful
    polybius("44324233521254134", false); //> false

## Substitution cipher
![Substitution Cipher](https://res.cloudinary.com/strive/image/upload/w_1000,h_1000,c_limit/19c12a6ee38ceddd82d75e12edf53189-image.png)

The substitution cipher requires a standard alphabet and a substitution alphabet. Letters from the standard alphabet will be transposed to the standard alphabet. This cipher requires that the recipient have the substitution alphabet, otherwise it will be difficult for them to decode the message.

For example, in the image above, the word HELLO would be translated as follows:

H becomes R.
E becomes M.
L becomes W.
O becomes L.
This would result in the code RMWWL. To decrypt this code, you would simply take the result and transpose back from the substitution alphabet to the standard alphabet.

    substitution(input,alphabet,encode=true)

The `substitution()` function in the src/substitution.js file has three parameters:

`input` refers to the inputted text to be encoded or decoded.
`alphabet` refers to substitution alphabet.
`encode` refers to whether you should encode or decode the message. By default it is set to `true`.

The `input` could include spaces and letters as well as special characters such as #, $, *, etc.
>Spaces should be maintained throughout.
>Capital letters can be ignored.  

Examples

    substitution("thinkful", "xoyqmcgrukswaflnthdjpzibev"); //> 'jrufscpw'
    substitution("You are an excellent spy", "xoyqmcgrukswaflnthdjpzibev"); //> 'elp xhm xf mbymwwmfj dne'
    substitution("jrufscpw", "xoyqmcgrukswaflnthdjpzibev", false); //> 'thinkful'
    
    substitution("message", "$wae&zrdxtfcygvuhbijnokmpl"); //> "y&ii$r&"
    substitution("y&ii$r&", "$wae&zrdxtfcygvuhbijnokmpl", false); //> "message"
    
    substitution("thinkful", "short"); //> false
    substitution("thinkful", "abcabcabcabcabcabcabcabcyz"); //> false
