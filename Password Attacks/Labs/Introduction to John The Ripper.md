## Use single-crack mode to crack r0lf's password.
```
echo 'r0lf:$6$ues25dIanlctrWxg$nZHVz2z4kCy1760Ee28M1xtHdGoy0C2cYzZ8l2sVa1kIa8K9gAcdBP.GI6ng/qA4oaMrgElZ1Cb9OeXO4Fvy3/:0:0:Rolf Sebastian:/home/r0lf:/bin/bash' > pass

john --single pass
```

## Use wordlist-mode with rockyou.txt to crack the RIPEMD-128 password
```
echo '193069ceb0461e1d40d216e32c79c704' > hash 

john --wordlist=/usr/share/wordlists/rockyou.txt --format=ripemd-128 hash
```
