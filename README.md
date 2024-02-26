# cryptography_19CS412_classical_techniques
CEASER CIPHER:

AIM :

To develope a simple Python program to implement ceaser cipher.

ALGORITHM :

Step 1 :

Design of Ceaser Cipher algorithm .

Step 2 :

Implementation using pyhton code .

Step 3 :

Testing algorithm with different key values .

PROGRAM:

```

def encrypt(text,s):
	result = ""


	for i in range(len(text)):
		char = text[i]

	
		if (char.isupper()):
			result += chr((ord(char) + s-65) % 26 + 65)

		
		else:
			result += chr((ord(char) + s - 97) % 26 + 97)

	return result


text = "POKALA GURAVAIAH"
s = 4
print ("Text : " + text)
print ("Shift : " + str(s))
print ("Cipher: " + encrypt(text,s))

```

OUTPUT:

![image](https://github.com/POKALAGURAVAIAH8121/cryptography_19CS412_classical_techniques/assets/128034765/cfed70bc-1eec-4827-ab40-b9aa0e665568)

RESULT:

Thus , The program is executed perfectly and output is verified.

PLAYFAIR CIPHER:

AIM :

To develop a simple Python Program to implement PlayFair Cipher.

ALGORITHM :

Step 1 :

Design of PlayFair Cipher algorithm.

Step 2 :

Now implement the Python program.

Step 3 :

Testing algorithm with different key values.

PROGRAM :

```

 
def toLowerCase(text):
    return text.lower()
 
# Function to remove all spaces in a string
 
 
def removeSpaces(text):
    newText = ""
    for i in text:
        if i == " ":
            continue
        else:
            newText = newText + i
    return newText
 
# Function to group 2 elements of a string
# as a list element
 
 
def Diagraph(text):
    Diagraph = []
    group = 0
    for i in range(2, len(text), 2):
        Diagraph.append(text[group:i])
 
        group = i
    Diagraph.append(text[group:])
    return Diagraph
 
# Function to fill a letter in a string element
# If 2 letters in the same string matches
 
 
def FillerLetter(text):
    k = len(text)
    if k % 2 == 0:
        for i in range(0, k, 2):
            if text[i] == text[i+1]:
                new_word = text[0:i+1] + str('x') + text[i+1:]
                new_word = FillerLetter(new_word)
                break
            else:
                new_word = text
    else:
        for i in range(0, k-1, 2):
            if text[i] == text[i+1]:
                new_word = text[0:i+1] + str('x') + text[i+1:]
                new_word = FillerLetter(new_word)
                break
            else:
                new_word = text
    return new_word
 
 
list1 = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'k', 'l', 'm',
         'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z']
 
# Function to generate the 5x5 key square matrix
 
 
def generateKeyTable(word, list1):
    key_letters = []
    for i in word:
        if i not in key_letters:
            key_letters.append(i)
 
    compElements = []
    for i in key_letters:
        if i not in compElements:
            compElements.append(i)
    for i in list1:
        if i not in compElements:
            compElements.append(i)
 
    matrix = []
    while compElements != []:
        matrix.append(compElements[:5])
        compElements = compElements[5:]
 
    return matrix
 
 
def search(mat, element):
    for i in range(5):
        for j in range(5):
            if(mat[i][j] == element):
                return i, j
 
 
def encrypt_RowRule(matr, e1r, e1c, e2r, e2c):
    char1 = ''
    if e1c == 4:
        char1 = matr[e1r][0]
    else:
        char1 = matr[e1r][e1c+1]
 
    char2 = ''
    if e2c == 4:
        char2 = matr[e2r][0]
    else:
        char2 = matr[e2r][e2c+1]
 
    return char1, char2
 
 
def encrypt_ColumnRule(matr, e1r, e1c, e2r, e2c):
    char1 = ''
    if e1r == 4:
        char1 = matr[0][e1c]
    else:
        char1 = matr[e1r+1][e1c]
 
    char2 = ''
    if e2r == 4:
        char2 = matr[0][e2c]
    else:
        char2 = matr[e2r+1][e2c]
 
    return char1, char2
 
 
def encrypt_RectangleRule(matr, e1r, e1c, e2r, e2c):
    char1 = ''
    char1 = matr[e1r][e2c]
 
    char2 = ''
    char2 = matr[e2r][e1c]
 
    return char1, char2
 
 
def encryptByPlayfairCipher(Matrix, plainList):
    CipherText = []
    for i in range(0, len(plainList)):
        c1 = 0
        c2 = 0
        ele1_x, ele1_y = search(Matrix, plainList[i][0])
        ele2_x, ele2_y = search(Matrix, plainList[i][1])
 
        if ele1_x == ele2_x:
            c1, c2 = encrypt_RowRule(Matrix, ele1_x, ele1_y, ele2_x, ele2_y)
            # Get 2 letter cipherText
        elif ele1_y == ele2_y:
            c1, c2 = encrypt_ColumnRule(Matrix, ele1_x, ele1_y, ele2_x, ele2_y)
        else:
            c1, c2 = encrypt_RectangleRule(
                Matrix, ele1_x, ele1_y, ele2_x, ele2_y)
 
        cipher = c1 + c2
        CipherText.append(cipher)
    return CipherText
 
 
text_Plain = 'SIDDANAGAIAH'
text_Plain = removeSpaces(toLowerCase(text_Plain))
PlainTextList = Diagraph(FillerLetter(text_Plain))
if len(PlainTextList[-1]) != 2:
    PlainTextList[-1] = PlainTextList[-1]+'z'
 
key = "POKALA"
print("Key text:", key)
key = toLowerCase(key)
Matrix = generateKeyTable(key, list1)
 
print("Plain Text:", text_Plain)
CipherList = encryptByPlayfairCipher(Matrix, PlainTextList)
 
CipherText = ""
for i in CipherList:
    CipherText += i
print("CipherText:", CipherText)
```
OUTPUT:

![image](https://github.com/POKALAGURAVAIAH8121/cryptography_19CS412_classical_techniques/assets/128034765/fe4e78d1-eb8d-40ea-bf4b-b98390962c5b)

RESULT :

Thus , The program is executed perfectly and output is verified.

HILL CIPHER

AIM :

To develop a simple Python Program to implement Hill Cipher.

ALGORITHM :

Step 1 :

First, develop the hill cipher program and design it.

Step 2 :

Now, implement the Python Program for the Hill Cipher Algorithm.

Step 3 :

Now, Make a Test for the different key values.

PROGRAM :
```
 
keyMatrix = [[0] * 3 for i in range(3)]
 
# Generate vector for the message
messageVector = [[0] for i in range(3)]
 
# Generate vector for the cipher
cipherMatrix = [[0] for i in range(3)]
 
# Following function generates the
# key matrix for the key string
def getKeyMatrix(key):
    k = 0
    for i in range(3):
        for j in range(3):
            keyMatrix[i][j] = ord(key[k]) % 65
            k += 1
 
# Following function encrypts the message
def encrypt(messageVector):
    for i in range(3):
        for j in range(1):
            cipherMatrix[i][j] = 0
            for x in range(3):
                cipherMatrix[i][j] += (keyMatrix[i][x] *
                                       messageVector[x][j])
            cipherMatrix[i][j] = cipherMatrix[i][j] % 26
 
def HillCipher(message, key):
 
    # Get key matrix from the key string
    getKeyMatrix(key)
 
    # Generate vector for the message
    for i in range(3):
        messageVector[i][0] = ord(message[i]) % 65
 
    # Following function generates
    # the encrypted vector
    encrypt(messageVector)
 
    # Generate the encrypted text 
    # from the encrypted vector
    CipherText = []
    for i in range(3):
        CipherText.append(chr(cipherMatrix[i][0] + 65))
 
    # Finally print the ciphertext
    print("Ciphertext: ", "".join(CipherText))
 
# Driver Code
def main():
 
    # Get the message to 
    # be encrypted
    message = "ACT"
 
    key = "GYBNQKURP"
 
    HillCipher(message, key)
 
if __name__ == "__main__":
    main()
```
OUTPUT:

![image](https://github.com/POKALAGURAVAIAH8121/cryptography_19CS412_classical_techniques/assets/128034765/c0b270d0-72d8-42a3-a5cc-0b57ff9e7b1a)

RESULT :

Thus , The program is executed perfectly and output is verified.

Vigenere Cipher

AIM :

To develop a simple python program to implement Vigenere Cipher.

ALGORITHM :

Step 1 :

First, develop the Vigenere cipher program and design it.

Step 2 :

Now, implement the Python Program for the Vigenere Cipher Algorithm.

Step 3 :

Now, Make a Test for the different key values.

PROGRAM :
```
# Python code to implement
# Vigenere Cipher

# This function generates the 
# key in a cyclic manner until 
# it's length isn't equal to 
# the length of original text
def generateKey(string, key):
	key = list(key)
	if len(string) == len(key):
		return(key)
	else:
		for i in range(len(string) -
					len(key)):
			key.append(key[i % len(key)])
	return("" . join(key))
	
# This function returns the 
# encrypted text generated 
# with the help of the key
def cipherText(string, key):
	cipher_text = []
	for i in range(len(string)):
		x = (ord(string[i]) +
			ord(key[i])) % 26
		x += ord('A')
		cipher_text.append(chr(x))
	return("" . join(cipher_text))
	
# This function decrypts the 
# encrypted text and returns 
# the original text
def originalText(cipher_text, key):
	orig_text = []
	for i in range(len(cipher_text)):
		x = (ord(cipher_text[i]) -
			ord(key[i]) + 26) % 26
		x += ord('A')
		orig_text.append(chr(x))
	return("" . join(orig_text))
	
# Driver code
if __name__ == "__main__":
	string = "GEEKSFORGEEKS"
	keyword = "AYUSH"
	key = generateKey(string, keyword)
	cipher_text = cipherText(string,key)
	print("Ciphertext :", cipher_text)
	print("Original/Decrypted Text :", 
		originalText(cipher_text, key))

# This code is contributed 
# by Pratik Somwanshi
```
OUTPUT:

![image](https://github.com/POKALAGURAVAIAH8121/cryptography_19CS412_classical_techniques/assets/128034765/96e7a4f8-c384-491c-bbc6-0d4b702d3d0a)

RESULT :

Thus , The program is executed perfectly and output is verified.

Rail Fence Cipher

AIM :

To develop a simple Python program to implement Rail Fence Cipher.

ALGORRITHM :

Step 1 :

To develop a simple python program to implement Rail Fence Cipher.

Step 2 :

Now, implement the Python Program for the Rail Fence Cipher Algorithm.

Step 3 :

Now, Make a Test for the different key values.

PROGRAM :
```

	# Python3 program to illustrate
# Rail Fence Cipher Encryption
# and Decryption

# function to encrypt a message
def encryptRailFence(text, key):

	# create the matrix to cipher
	# plain text key = rows ,
	# length(text) = columns
	# filling the rail matrix
	# to distinguish filled
	# spaces from blank ones
	rail = [['\n' for i in range(len(text))]
				for j in range(key)]
	
	# to find the direction
	dir_down = False
	row, col = 0, 0
	
	for i in range(len(text)):
		
		# check the direction of flow
		# reverse the direction if we've just
		# filled the top or bottom rail
		if (row == 0) or (row == key - 1):
			dir_down = not dir_down
		
		# fill the corresponding alphabet
		rail[row][col] = text[i]
		col += 1
		
		# find the next row using
		# direction flag
		if dir_down:
			row += 1
		else:
			row -= 1
	# now we can construct the cipher
	# using the rail matrix
	result = []
	for i in range(key):
		for j in range(len(text)):
			if rail[i][j] != '\n':
				result.append(rail[i][j])
	return("" . join(result))
	
# This function receives cipher-text
# and key and returns the original

def decryptRailFence(cipher, key):

	# create the matrix to cipher
	# plain text key = rows ,
	# length(text) = columns
	# filling the rail matrix to

	rail = [['\n' for i in range(len(cipher))]
				for j in range(key)]
	
	# to find the direction
	dir_down = None
	row, col = 0, 0
	
	# mark the places with '*'
	for i in range(len(cipher)):
		if row == 0:
			dir_down = True
		if row == key - 1:
			dir_down = False
		
		# place the marker
		rail[row][col] = '*'
		col += 1
		
		# find the next row
		# using direction flag
		if dir_down:
			row += 1
		else:
			row -= 1
			
	# now we can construct the
	# fill the rail matrix
	index = 0
	for i in range(key):
		for j in range(len(cipher)):
			if ((rail[i][j] == '*') and
			(index < len(cipher))):
				rail[i][j] = cipher[index]
				index += 1
		
	# now read the matrix in
	# zig-zag manner to construct
	# the resultant text
	result = []
	row, col = 0, 0
	for i in range(len(cipher)):
		
		# check the direction of flow
		if row == 0:
			dir_down = True
		if row == key-1:
			dir_down = False
			
		# place the marker
		if (rail[row][col] != '*'):
			result.append(rail[row][col])
			col += 1
			
		# find the next row using
		# direction flag
		if dir_down:
			row += 1
		else:
			row -= 1
	return("".join(result))

# Driver code
if __name__ == "__main__":
	print(encryptRailFence("attack at once", 2))
	print(encryptRailFence("GeeksforGeeks ", 3))
	print(encryptRailFence("defend the east wall", 3))
	
	print(decryptRailFence("GsGsekfrek eoe", 3))
	print(decryptRailFence("atc toctaka ne", 2))
	print(decryptRailFence("dnhaweedtees alf tl", 3))
```

OUTPUT:

![image](https://github.com/POKALAGURAVAIAH8121/cryptography_19CS412_classical_techniques/assets/128034765/07cba90d-c12b-4e75-8dfd-07c908b4724e)

RESULT :

Thus , The program is executed perfectly and output is verified.
