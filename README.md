/============================= GREP DEMO ====================================
***

# =============== GREP ================
- **grep** = Global Regular Expression Printer  
- **grep** is used to search a particular pattern in files or folders  

***

# ========== Syntax of GREP ============
```bash
grep [flags] [pattern] [file/folder]
```
***

We have many flags that can be used with `grep`.  
Here’s a **mnemonic** to remember some important ones:

**CODE = i nEVER cOUNTED rED oR vIOLET eRRORS and wORDS**

Let’s explore each flag step by step.

***

### Create a sample file
```bash
$ echo -e "apple\nApple\nAPPLE\nBANANA\nBanana\nOrange" >> fruits.txt
$ cat fruits.txt
apple
Apple
APPLE
BANANA
Banana
Orange
```

***

### Basic search
```bash
$ grep "apple" fruits.txt
```
**o/p**
```
apple
```

- Only **lowercase apple** matched because grep is case-sensitive.  
- To make it case-insensitive, use **-i**:

```bash
$ grep -i "apple" fruits.txt
```
**o/p**
```
apple
Apple
APPLE
```

***

# =============== FLAG EXAMPLES ===============

## FLAG: `-n`
Show line number of match  
```bash
$ grep -n "Banana" fruits.txt
```
**o/p**
```
5:Banana
```
👉 Match found on line 5.

***

## FLAG: `-c`
Count matches  
```bash
$ grep -c "Apple" fruits.txt
```
**o/p**
```
2
```
👉 Matches both "Apple" and "APPLE".

***

## FLAG: `-r`
Recursive search through folders  
```bash
$ mkdir testdir && mv fruits.txt testdir/
$ grep -r "Orange" testdir/
```
**o/p**
```
testdir/fruits.txt:Orange
```

***

## FLAG: `-o`
Print only the matched part (not the whole line)  
```bash
$ grep -o "Apple" fruits.txt
```
**o/p**
```
Apple
APPLE
```

***

## FLAG: `-v`
Invert the match (show lines *without* the pattern)  
```bash
$ grep -v "apple" fruits.txt
```
**o/p**
```
Apple
APPLE
BANANA
Banana
Orange
```

***

## FLAG: `-E`
Enable extended regex  
```bash
$ grep -E "apple|Banana" fruits.txt
```
**o/p**
```
apple
Banana
```

***

## FLAG: `-w`
Match only **whole words**  
```bash
$ grep -w "app" fruits.txt
```
**o/p**
```
(nothing)
```

```bash
$ grep -w "apple" fruits.txt
```
**o/p**
```
apple
```

***

#================================ 🔎 Review Questions (Practice)====================================================

# Now lets see some of the review Questions in our curricum

## 1️⃣ Get last **x** lines from a file (e.g., Harry Potter text)  
```bash
$ tail -n 20 harry.txt | grep -o -i "harry"
```
👉 tail Displays the last **20 lines** of `harry.txt` and gives the output through pipe to grep then
   grep will search and prints the "harry" only
***

## 2️⃣ Get word counts for specific words in `harry.txt`
```bash
$ grep -o "Harry" harry.txt | wc -l
$ grep -o "ron" harry.txt | wc -l
$ grep -o "dumbledore" harry.txt | wc -l
$ grep -o "Hermione" harry.txt | wc -l
```
now will do all the operations in one command
```bash
$ grep -o -i -E "Harry|ron|dumbledore" harry.txt |sort|uniq -c
```

👉 Counts occurrences of each word.  

For regex (ron **or** dumbledore together):
```bash
$ grep -E -o "ron|dumbledore" harry.txt | wc -l
```

***

## 3️⃣ Find PID of Firefox Browser
```bash
$ pgrep firefox
```
OR
```bash
$ ps aux | grep firefox
```

***

## 4️⃣ Parent Process vs. Child Process  
- **Parent Process** → The original process that creates another process.  
- **Child Process** → The process created by the parent.  
- They communicate often using **pipes**.  

Example with pipe:
```bash
$ ps -ef | grep firefox
```

***

## 5️⃣ Kill a process using pipes (`grep + awk + xargs + kill`)
Find & kill Firefox in one line:
```bash
$ ps -ef | grep firefox | awk '{print $2}' | xargs kill -9
```
- `awk '{print $2}'` → extracts the PID column  
- `xargs kill -9` → kills those processes  

***

## 6️⃣ Use `find` to locate files
Go to **home folder**:
```bash
$ cd ~
```
Find all files or directories containing **java** in their name:
```bash
$ find . -iname "*java*"
```

***

## 🎯 Quick Word Search Practice (`harry.txt`)

Search for these words using `grep`:
```text
Harry
ron
dumbledore
Hermione
```

Example:
```bash
$ grep -i "Harry" harry.txt | wc -l
```
👉 Counts all occurrences of **Harry** .

***

✨ These review questions combine **grep, pipes, process handling, and find command** for hands-on practice.  


#============== 

# GREP Summary Table

| Flag | Meaning                        | Example                     | Output/Effect                           |
|------|--------------------------------|-----------------------------|-----------------------------------------|
| `-i` | Ignore case sensitivity        | `grep -i "apple" fruits.txt` | Matches apple, Apple, APPLE             |
| `-n` | Show line numbers              | `grep -n "Banana" fruits.txt` | `5:Banana`                             |
| `-c` | Count matches                  | `grep -c "Apple" fruits.txt` | `2`                                    |
| `-r` | Recursive search in folders    | `grep -r "Orange" testdir/`  | `testdir/fruits.txt:Orange`            |
| `-o` | Show only matched part         | `grep -o "Apple" fruits.txt` | Apple <br> APPLE                       |
| `-v` | Invert match (exclude pattern) | `grep -v "apple" fruits.txt` | Prints all lines **except** apple       |
| `-E` | Extended regex support         | `grep -E "apple\|Banana" fruits.txt` | apple <br> Banana            |
| `-w` | Match whole words only         | `grep -w "apple" fruits.txt` | apple (but not app or apple123)         |

***
