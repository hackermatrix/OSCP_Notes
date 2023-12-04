# Parameter Discovery

#### 1. waybackurls:

```
waybackurls example.com
```

* The command will fetch all the urls associated with example.com.

```
grep -oP ‘(?<=\?|&)\w+(?==|&)’ urls.txt | sort -u
```

* The above command can be used to extract parameters from all of the urls.

#### References:

[https://aswinthambipanik07.medium.com/bug-bounty-recon-part-4-d52d2215f1c](https://aswinthambipanik07.medium.com/bug-bounty-recon-part-4-d52d2215f1c)
