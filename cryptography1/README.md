# Cryptography
*Encryption* is the process of encoding data in a way that only authorized people can read it. This is used to secure data and prevent it from being read by prying eyes. When encrypted data is received, it can be *decrypted* if we have the key.

To *encrypt* (also informally known as *scramble*) is to apply an encryption algorithm to each of the characters in the *plaintext* (unencrypted) message in order to conceal its meaning. To *decrypt* (descramble) is to use the key to apply the same algorithm in reverse to the encrypted message to reveal the plaintext message. If we use a good algorithm, even if our message is intercepted, it can’t be read if the person in who interecpted it doesn't have the key.

This is called a *cipher*. The word originated in the late 14th century from the Arabic word sifr, meaning “zero.”  Despite its more recent name, ciphers have been used for thousands of years. Julius Caesar used a simple one, which we know as a Caesar Cipher (more on this later).

### Substitution Ciphers
In a substitution cipher, letters in the plaintext message are replaced with other letters, according to a fixed system.

### Transposition Ciphers
In a transposition cipher, the letters in the plaintext message are not replaced, but are switched around so that the message can't be easiliy read.
<br><br>

## Letters as Numbers
Computers store everything as numbers, including characters (letters, digits, punctuation, emoji, etc.). This makes it easy to apply arithmetic algorithms to the characters; underneath, they're just numbers.
<br><br>
Try it out. Enter a number to see what the corresponding character is. Good ones to try are:
* 65
* 97
* 35
* 171
* 129312
* 128077

<div style="background-color:lightblue; padding:20px; width:300px;">
	Input number: 
	<input id="ordNumberInput" type="number" min="0" value="65" size="30"><br>
	<input type="button" value="Click to Convert" onclick="convertToEmoji();">
	<div id="emojiOutput" style="width:100px; font-size:48px;">&nbsp;</div>
<br></div>

<script>
	function convertToEmoji(){
		var num = document.getElementById("ordNumberInput").value;
		var emoji = String.fromCharCode(num);
		emoji = '&#x'+num
		document.getElementById('emojiOutput').innerText = String.fromCodePoint(num);;
	}
</script>

### ord() and chr()
In Python, the `ord()` function takes an ASCII character (the characters you can type on the keyboard) and returns the equivalent number.  The `chr()` function takes a number in the range 0-127 and returns the equivalent character.
Thus, `ord('a')` produces 97
and `chr(97)` prouces 'a'

{% next %}

# Caesar Cipher
The Caesar Cipher, one of the earliest known and simplest ciphers, is a special type of substituion cipher called a *rotation cipher*. Each letter in the plaintext message is 'shifted' a certain number of places down the alphabet. For example, with a shift of 2, A would be replaced by C, B would be replaced by D, and so on.

### Try enciphering the word *cipher* with a shift of 3. 
Enter your answer below:

<div style="background-color:lightblue; padding:20px; width:300px;">
	Input ciphertext: 
	<input id="textInput1" type="text"><br>
	<input type="button" value="Check Your Answer" onclick="checkAnswer();">
	<div id="output1" style="width:200px;"> </div>
<br></div>

<script>
	function checkAnswer(){
		var txt = document.getElementById("textInput1").value;
		if (txt == 'flskhu'){
		  document.getElementById('output1').innerText = 'Correct!';
	  } else {
      document.getElementById('output1').innerText = 'Incorrect. Try Again';
    }
  }
</script>
<br><br>
### Try encrypting any message, with a shift of your choice:
<div style="background-color:lightblue; padding:20px; width:400px;">
	Plaintext: 
	<input id="textInput2" type="text"><br>
	Choose a shift:
	<input id="shiftInput" type="number" width="20"><br>
	<input type="button" value="Encrypt" onclick="encipherCaesar();">
	<div id="output2" style="width:200px;">&nbsp; </div>
<br></div>


<script>
	function encipherCaesar(){
      	var plaintext = document.getElementById("textInput2").value;
      	var shift = document.getElementById("shiftInput").value % 26;
      	var ciphertext = "";
      	document.getElementById('output2').innerText = "encrypting...";
      	for (var i=0; i<plaintext.length; i++){
        	var chr = plaintext[i];
		var ordNum = 0;
		if (chr >= 'a' && chr <= 'z'){
	  		ordNum = chr.charCodeAt(0) + shift;
          		if (ordNum > 'z'.charCodeAt(0)){
	    			ordNum = ordNum - 26;
          		} else if (ordNum < 'a'.charCodeAt(0)){
	     			ordNum = ordNum + 26;
          		}
		} else if (chr >= 'A' && chr <= 'Z'){
	  		ordNum = chr.charCodeAt(0) + shift;
          		if (ordNum > 'Z'.charCodeAt(0)){
	    			ordNum = ordNum - 26;
          		} else if (ordNum < 'A'.charCodeAt(0)){
	    			ordNum = ordNum + 26;
          		}
		} else {
	  		ordNum = chr.charCodeAt(0);
		}
        	ciphertext += String.fromCharCode(ordNum);
      	}		
      	document.getElementById('output2').innerText = ciphertext;
    }
  
</script>

#### Play with this a bit:
* What happens if you encrypt the letter "x" with a shift of 5? 
* What happens if you try a negative shift? 
* What happens if your message contains punctuation or spaces? Do those get encrypted? 
* What happens if you mix uppercase and lowercase letters?
<br>

{% next %}
# Write a Caesar Cipher Function
Try writing a *function* to encrypt a message using the Caesar cipher.
Call the function `encrypt()`. It should do the following:
* take in a message as an argument (string)
* take in a shift as an argument (integer)
* return the encrypted message (string)
<br>

### Small Steps
A good place to start is to write a function to encrypt a single letter. Call this function `encryptLetter()`. It should take in a letter and a shift, and return the encrypted letter. The `encrypt()` function can call `encryptLetter()` over and over.

1. Type your function definitions in the `caesar.py` file to the right. 
2. After the function definitions, add some code to test your function, for example: `print(encrypt('hello', 5))`
3. To run your code, type `python caesar.py` in the terminal window at the bottom.

### Special Cases
When playing with the enciphering tool, it was suggested that you try some different cases. You'll need to modify your `encryptLetter()` function to deal with each of these cases:<br><br>
**Wraparound** <br>
If you encrypt the letter 'z' with a shift of one, it should become the letter 'a'. However, ord('z') is 122. If you add a shift of 1, you get 123. The character associated with 123 is the open curly bracket, which looks like this: {. Clearly not the letter 'a'! In this case, you'd need to subtract 26 (the number of letters in the alphabet) to get from 123 to 98, which is the number associated with 'a'. Change your `encryptLetter()` function so it handles wraparound. 
{% spoiler "Help" %}
If, after adding the shift, the number is bigger than ord('z'), subtract 26 from it before converting it back to a character.
{% endspoiler %}<br>
**Big Shift** <br>
If your shift is greater than the number of letters in the alphabet, your fix for special case 1 won't work. A shift of 28, for example, should work the same as a shift of 8. Modify your `encryptLetter()` function to handle shifts of any size.
{% spoiler "Help" %}
You can use Python's modulo operator to return the remainder of a division operation. 28%26 (28 divided by 26) yields a remainder of 2, so a shift of 28 would be converted to a shift of 2.  
{% endspoiler %}<br>
**Negative Shift** <br>
The same wraparound can happen if you allow negative shifts. The letter 'b' with a shift of -3 should be encrypted as 'y'. Modify your `encryptLetter()` function to allow negative shifts. Make sure to allow for wraparounds in the negative direction!
{% spoiler "Help" %}
If, after adding the shift (whether negative or positive), the number is less than ord('a'), add 26 from it before converting it back to a character.
{% endspoiler %}<br>
**Uppercase Letters** <br>
Your `encryptLetter()` function should handle uppercase as well as lowercase letters. Think how this might affect your wraparound.
{% spoiler "Help" %}
Use an if statement to separate out uppercase and lowercase letters and treat each case separately. A letter is uppercase if letter >= 'A' and letter <= 'Z'. A letter is lowercase if letter >= 'a' and letter <= 'z'.
{% endspoiler %}<br>
**Non-alphabetic Characters** <br>
For this exercise, punctuation and spaces -- anything that's not a letter -- shouldn't be encrypted. Modify your `encryptLetter()` function so that it only encrypts letters. All other characters should be returned unchanged.
{% spoiler "Help" %}
Add another case to your if statement so that if the letter is not uppercase and it's not lowercase, you return it unchanged.
{% endspoiler %}

{% next %}
# Decrypting the Caesar Cipher
In a rotation cipher like the Caesar Cipher, decrypting is equivalent to encrypting with the negative key. A message that's encrypted with a key (shift) of 5 can be decrypted using the same function, using a key of -5.

<br>
## ROT13
ROT13 is a Caesar cipher with a key of 13. It's used in online forums to hide spoilers, the punchlines to jokes, puzzle solutions, and the like from being casually or accidentally seen. It provides almost no cryptographic security -- everyone knows the key! Notice that to decrypt a message that has been encoded with ROT13, you just encrypt it again with a key of 13. In other words ROT13(ROT14(*x*))=*x*.

<br>
# Cracking the Caesar Cipher
The Caesar Cipher isn't a very secure way to encrypt messages. It can be easily broken using a brute-force method; after all, there are only 26 possible keys.<br><br>
For example, if you interecpted the following encrypted message:<br>
*iyeb ryfobmbkpd sc pevv yp oovc*<br>
you could just try every shift from 1 to 25:<br>
shift=0: *iyeb ryfobmbkpd sc pevv yp oovc* (this is the same as the original, but included here for the sake of completeness)<br>
shift=1: *jzfc szgpcnclqe td qfww zq ppwd* <br>
shift=2: *kagd tahqdodmrf ue rgxx ar qqxe* <br> 
shift=3: *lbhe ubirepensg vf shyy bs rryf* <br> 
shift=4: *mcif vcjsfqfoth wg tizz ct sszg* <br> 
shift=5: *ndjg wdktgrgpui xh ujaa du ttah* <br> 
shift=6: *oekh xeluhshqvj yi vkbb ev uubi* <br> 
shift=7: *pfli yfmvitirwk zj wlcc fw vvcj* <br> 
shift=8: *qgmj zgnwjujsxl ak xmdd gx wwdk* <br> 
shift=9: *rhnk ahoxkvktym bl ynee hy xxel* <br> 
shift=10: *siol bipylwluzn cm zoff iz yyfm* <br> 
shift=11: *tjpm cjqzmxmvao dn apgg ja zzgn* <br> 
shift=12: *ukqn dkranynwbp eo bqhh kb aaho* <br> 
shift=13: *vlro elsbozoxcq fp crii lc bbip* <br> 
shift=14: *wmsp fmtcpapydr gq dsjj md ccjq* <br> 
shift=15: *xntq gnudqbqzes hr etkk ne ddkr* <br> 
shift=16: *your hovercraft is full of eels* <br> 
shift=17: *zpvs ipwfsdsbgu jt gvmm pg ffmt* <br> 
shift=18: *aqwt jqxgtetchv ku hwnn qh ggnu* <br> 
shift=19: *brxu kryhufudiw lv ixoo ri hhov* <br> 
shift=20: *csyv lszivgvejx mw jypp sj iipw* <br> 
shift=21: *dtzw mtajwhwfky nx kzqq tk jjqx* <br> 
shift=22: *euax nubkxixglz oy larr ul kkry* <br> 
shift=23: *fvby ovclyjyhma pz mbss vm llsz* <br> 
shift=24: *gwcz pwdmzkzinb qa nctt wn mmta* <br> 
shift=25: *hxda qxenalajoc rb oduu xo nnub* <br> 
Upon inspection, it's clear that the message was enciphered with a key of 10 because 26-16=10.<br><br>

## Write a Caesar Cipher Cracker
Write a function that takes an encrypted message and prints out all 26 possible decryptions. Try it on this message:<br>
R cqrwt hxd qjen cqn qjwp xo cqrb!
<br><br>
### [Next: Substitution Ciphers](https://lab.cs50.io/martybillingsleyucls/uclsPython/master/cryptography2/)



