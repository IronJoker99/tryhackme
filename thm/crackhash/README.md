# HASH CAT TOOL USAGE
	
	In hash cat tool we can encrypt and decrypt the cipher text.
	Here, is attack mode and hash type flags are requare, -a is attack, -m is hash type.
	


# hash commands example
## MD5
	for md5 we have the attack is 0, 
```bash
hashcat -a 0 -m 0  48bb6e862e54f2a795ffc4e541caed4d /usr/share/SecLists/rockyou.txt
```
48bb6e862e54f2a795ffc4e541caed4d: easy

## 	For a sha mode
```bash
hashcat -a 0 -m 100 CBFDAC6008F9CAB4083784CBD1874F76618D2A97 /usr/share/SecLists/rockyou.txt
```
CBFDAC6008F9CAB4083784CBD1874F76618D2A97 : password123


## FOR SHA2-256
```bash
hashcat -a 0 -m 1400 1C8BFE8F801D79745C4631D09FFF36C82AA37FC4CCE4FC946683D7B336B63032 /usr/share/SecLists/rockyou.txt
```
one more example
```bash
hashcat -a 0 -m 1400 F09EDCB1FCEFC6DFB23DC3505A882655FF77375ED8AA2D1C13F640FCCC2D0C85  /usr/share/SecLists/rockyou.txt
```

F09EDCB1FCEFC6DFB23DC3505A882655FF77375ED8AA2D1C13F640FCCC2D0C85:paule 
1C8BFE8F801D79745C4631D09FFF36C82AA37FC4CCE4FC946683D7B336B63032:letmein

## F0or the bcrypt $2*$, Blowfish (Unix) 
```bash
hashcat -a 0 -m 3200 $2y$12$Dwt1BZj6pcyc3Dy1FWZ5ieeUznr71EeNkJkUlypTsgbX1H68wsRom  /usr/share/SecLists/rockyou.txt
```
3200


## for the MD4 hash
```bash
hashcat -a 0 -m 900 279412f945939ba78ce0758d3fd83daa /usr/share/SecLists/rockyou.txt
```
but there is error on it, why, because the rockyou file does not have password. we need to try a md4 online.

## hash type NTLM
```bash
hashcat -a 0 -m 3000 1DFECA0C002AE40B8619ECF94819CC1B /usr/share/SecLists/rockyou.txt
``` 
1DFECA0C002AE40B8619ECF94819CC1B:n63umy8lkf4i: 

##

```bash
hashcat -a 0 -m 1800 $6$aReallyHardSalt$6WKUTqzq.UQQmrm0p/T7MPpMbGNnzXPMAXi4bJMl9be.cfi3/qxIf.hsGpS41BqMhSrHVXgMpdjS6xeKZAs02. /usr/share/SecLists/rockyou.txt
```

$6$aReallyHardSalt$6WKUTqzq.UQQmrm0p/T7MPpMbGNnzXPMAXi4bJMl9be.cfi3/qxIf.hsGpS41BqMhSrHVXgMpdjS6xeKZAs02.: 

 ##
```bash
hashcat -a 0 -m 160 e5d8870e5bdd26602cab8dbe07a942c8669e56d6  /usr/share/SecLists/rockyou.txt
```

e5d8870e5bdd26602cab8dbe07a942c8669e56d6:


