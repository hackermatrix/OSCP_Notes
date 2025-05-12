# Creating Customized Wordlists

1. **Cewl** crawls through the target website and extracts keywords

```bash
cewl -w list.txt -d 5 -m 5 http://thm.labs
```

2. **username\_generator** can be used to generate usernames based on firstname and lastname

```bash
python3 username_generator.py -w users.lst
```

3. **Crunch** can be used to create wordlist based on permuation and combination of alphabets, num and symbols

```
crunch <min-len> <max-len> [<charset string>]

e.g
1. crunch 2 2 01234abcd -o crunch.txt
2. crunch 6 6 -t pass%%
```

4. #### CUPP - Common User Passwords Profiler can use things like : birthdate, pet name ,etc to generate passwords.

#### &#x20;-  [https://github.com/Mebus/cupp](https://github.com/Mebus/cupp)

## # 5. HashCat :cat::

```bash
 - [ Attack Modes ] -                    
 
  # | Mode
 ===+======
  0 | Straight
  1 | Combination
  3 | Brute-force
  6 | Hybrid Wordlist + Mask
  7 | Hybrid Mask + Wordlist
  9 | Association

- [ Built-in Charsets ] -

  ? | Charset
 ===+=========
  l | abcdefghijklmnopqrstuvwxyz [a-z]
  u | ABCDEFGHIJKLMNOPQRSTUVWXYZ [A-Z]
  d | 0123456789                 [0-9]
  h | 0123456789abcdef           [0-9a-f]
  H | 0123456789ABCDEF           [0-9A-F]
  s |  !"#$%&'()*+,-./:;<=>?@[\]^_`{|}~
  a | ?l?u?d?s
  b | 0x00 - 0xff

# 1. Dictionary Attack:
hashcat -a 0 -m 0 <_hash_> /usr/share/wordlists/rockyou.txt
(-a 0 is for dictionary attack mode )

# 2. BruteForce Attack:
hashcat -a 3 -m 0 <hash> ?d?d?d?d (using the charset i.e 4 numbers 0000 to 9999)

```

## Rule-Based attacks :notebook::

```bash
john --wordlist=single-password-list.txt --rules=KoreLogic
```
