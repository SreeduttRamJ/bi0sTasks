# Automate-the-Boring-Stuff-Writeup

<h3>Chapter 5 - Dictionaries and structuring data</h3>

<h4>Practice Questions</h4><br></br>

1. What does the code for an empty dictionary look like?

```
d={}
```

2. What does a dictionary value with a key 'foo' and a value 42 look like?

```
d={"foo":42}
```

3. What is the main difference between a dictionary and a list?

|List|Dictionary|
|:------------:|:-----------:|
|collection of index values pairs|collection of key value pairs|
|place elements in [ ] separated by commas(,)|place elements in { } as “key”:”value”,separated by commas(,)|
|value accesed using indices starting from 0|values accesed using keys|
|element order is maintained|element order may not be maintained|


4. What happens if you try to access spam['foo'] if spam is {'bar': 100}?

```
It shows a keyerror
```
![image](https://user-images.githubusercontent.com/113903135/217070393-27a70e59-01e4-4051-98f5-77ca2a1c7c3a.png)

5. If a dictionary is stored in spam, what is the difference between the expressions 'cat' in spam and 'cat' in spam.keys()?

```
Both returns same value as both expressions check if a key named 'cat' is present in spam
```
![image](https://user-images.githubusercontent.com/113903135/217070952-2b2ef455-f516-4a68-bd63-ca215dc633f3.png)

6. If a dictionary is stored in spam, what is the difference between the expressions 'cat' in spam and 'cat' in spam.values()?

```
first expression check for a key named 'cat' while second expression check for value named 'cat'
```

![image](https://user-images.githubusercontent.com/113903135/217071743-0c1af3eb-4ad6-4c82-878e-ee6a85fb1288.png)

7. What is a shortcut for the following code?

if 'color' not in spam: spam['color'] = 'black'

```
spam.setdefault('color', 'black')
```
![image](https://user-images.githubusercontent.com/113903135/217072235-c39550f4-8c5f-495a-a118-21757e17a8a1.png)

8. What module and function can be used to “pretty print” dictionary values?

```
we use the module pprint and function pprint()
```

<h3>Practice Projects</h3>

<h4>Chess Dictionary Validator</h4>

In this chapter, we used the dictionary value {'1h': 'bking', '6c': 'wqueen', '2g': 'bbishop', '5h': 'bqueen', '3e': 'wking'} to represent a chess board. Write a function named isValidChessBoard() that takes a dictionary argument and returns True or False depending on if the board is valid.

A valid board will have exactly one black king and exactly one white king. Each player can only have at most 16 pieces, at most 8 pawns, and all pieces must be on a valid space from '1a' to '8h'; that is, a piece can’t be on space '9z'. The piece names begin with either a 'w' or 'b' to represent white or black, followed by 'pawn', 'knight', 'bishop', 'rook', 'queen', or 'king'. This function should detect when a bug has resulted in an improper chess board.

> ANSWER
```
def isValidChessBoard(d):
    bpiece=0
    wpiece=0
    for i in d.values():
        if i[0]=='w':
            wpiece=wpiece+1
        elif i[0]=='b':
            bpiece=bpiece+1
        else:
            return False
    if bpiece != 16 or wpiece != 16:
        return False
    for i in d.keys():
        if i[0]>8 or i[1] not in ['a','b','c','d','e','f','g','h']:
            return False
    lw=['king','queen','knight','knight','bishop','bishop','rook','rook','pawn']        
    lb=['king','queen','knight','knight','bishop','bishop','rook','rook','pawn']
    bp=wp=8
    for i in d.values():
        if i[0]=='w' and i[1:] in lw:
             if i[1:]=='pawn' and wp!=0:
                 wp=wp-1
             else:
                 lw.remove(i[1:])
        elif i[0]=='b' and i[1:] in lb:
            if i[1:]=='pawn' and bp!=0:
                 bp=bp-1
            else:
                 lb.remove(i[1:])
        else:
            return False
    return True

    


chess={'1h': 'king', '6c': 'wqueen', '2g': 'bbishop', '5h': 'bqueen', '3e': 'wking'}
print(isValidChessBoard(chess))
```
