# S3 buckets

### Step 1:

Find Subdomains for the target.

### Step 2:

```
ffuf -u http://FUZZ.s3.amazonaws.com -w subdomains.txt
```

* Bruteforce the lis of subs for s3 buckets.

### Step 3:

```
aws s3 ls s3://sub.redacted.com
```

* Use AWS CLI to perform actions.

#### References:

* [https://aswinthambipanik07.medium.com/playing-with-s3-leaks-2c5a0dda6014](https://aswinthambipanik07.medium.com/playing-with-s3-leaks-2c5a0dda6014)
