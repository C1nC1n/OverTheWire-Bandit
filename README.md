# OverTheWire-Bandit Wargame

###  
Per pastarąjį mėnesį  nuosekliai gilinausi į Pentesting. Intensyviai tyrinėju šią sritį, praktikuojuosi ir tobulinu savo pagrindinio lygio Linux įgūdžius, taip pat plečiu žinias apie įvairius įrankius.

## Level 0

Nulinis lygis yra gana lengvas – visa užduotis yra prisijungti prie laboratorijos naudojant ssh komandą ir pateiktus prisijungimo duomenis.

<img width="482" alt="Screenshot 2024-07-13 at 13 32 43" src="https://github.com/user-attachments/assets/c1bc0a1a-028a-46af-a3de-ed317f29cc03">

## Level 0  > 1

The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

Randame slaptažodį naudodami ls ir cat readme komandas.

<img width="424" alt="Screenshot 2024-07-13 at 13 38 38" src="https://github.com/user-attachments/assets/51186e5f-d572-4742-9332-08044dd0f2d5">

Atsijungiame nuo bandit0 ssh ir jungiamės per ssh į bandit1@bandit.labs.overthewire.org, naudodami rastą slaptažodį.

<img width="489" alt="Screenshot 2024-07-13 at 13 58 29" src="https://github.com/user-attachments/assets/9a0454f8-4eef-4980-bcd6-4e0905611261">

## Level 1 > 2 

The password for the next level is stored in a file called - located in the home directory

Nemeluosiu, teko googlinti, kaip atidaryti failą, jei jo pavadinimas simbolis.

cat < -filename :) 

Taip ranud bandit 2 slaptazodi.

<img width="446" alt="Screenshot 2024-07-13 at 14 01 23" src="https://github.com/user-attachments/assets/7bf9cb68-ae56-44fb-a6b0-51a4f1ff1dde">

## Level 2 > 3
The password for the next level is stored in a file called spaces in this filename located in the home directory

Cia randu failus ir juos atidarau taip gaunu slaptazodi 

<img width="439" alt="Screenshot 2024-07-13 at 18 25 53" src="https://github.com/user-attachments/assets/85df8107-358f-4775-8c19-ae63505f1723">

## Level 3 > 4

The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

Atsidarius bandit3, naudojau komandą ls, kuri parodė, kad yra direktorija inhere.

Vėl bandau ls, bet šį kartą nieko nerodo, tad panaudoju ls -a, kuri rodo paslėptus failus ir prasidedančius tašku.

Ten randu katalogą ... Hiding-From-You.

Atidarau failą ir randu dar vieną slaptažodį į kitą bandit lygį.

<img width="413" alt="Screenshot 2024-07-13 at 18 31 27" src="https://github.com/user-attachments/assets/c64f3861-11cc-4362-9840-919c0001ec34">

## Level 4 > 5

The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

human-readable
1033 bytes in size
not executable

Naudojau kitą komandą file ./*, kuri nustato failų tipus, o ./* nurodo visus failus dabartinėje direktorijoje.


<img width="487" alt="Screenshot 2024-07-13 at 18 58 04" src="https://github.com/user-attachments/assets/74445eba-df81-4ccb-86b3-d4ec3132faa5">

## Level 5 > 6

The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:
human-readable
1033 bytes in size
not executable

Atsidarau inhere direktoriją ir, pagal užduotį, pasirenku ieškoti failo pagal dydį. Tai padarau naudodamas komandą find -type f -size 1033c.

<img width="484" alt="Screenshot 2024-07-13 at 19 21 40" src="https://github.com/user-attachments/assets/6015540a-8419-464f-a5d8-287bcc4e6d41">

## Level 6 > 7 

The password for the next level is stored somewhere on the server and has all of the following properties:
owned by user bandit7
owned by group bandit6
33 bytes in size

Naudoju find, kad surastų bandit7 vartotoją, kuris yra bandit6 grupėje ir failo dydis yra 33 baitai:

find / -user bandit7 -group bandit6 -size 33c 2>/dev/null

Tačiau gaunu daug klaidų dėl leidimų (Permission denied), todėl pridedu 2>/dev/null, kad nukreipti klaidų pranešimus, ir randu atsakymą, kur slypi mano kitas slaptažodis:

/var/lib/dpkg/info/bandit7.password

<img width="487" alt="Screenshot 2024-07-13 at 19 36 05" src="https://github.com/user-attachments/assets/e5aaaa80-e8af-4e5c-8422-173a8965224a">

## Level 7 > 8

The password for the next level is stored in the file data.txt next to the word millionth

Atidarius data.txt puslapyje daug vardu ir slaptažodziu tai tiesiog atrinkti millionth naudojau grep komanda

cat data.txt | grep millionth 

<img width="485" alt="Screenshot 2024-07-13 at 19 39 22" src="https://github.com/user-attachments/assets/8decf9fc-86ad-4a2b-be71-c5eda3aaeffb">

## Level 8 > 9 

The password for the next level is stored in the file data.txt and is the only line of text that occurs only once.

Galvojau, kol nepradėjau gilintis į duotus komandų pavyzdžius, kaip naudoti uniq.

Naudojau komandą sort data.txt | uniq -c, kuri surūšiuoja data.txt teksto eilutes ir paskaičiuoja, kiek kartų kiekviena eilutė pasikartojo. Patikrines rezultatus, radau, kad vienas slaptažodis pasikartojo tik vieną kartą, ko ir ieškojau.

Pagalvojau, kad jei būtų daugiau tokio teksto, būtų nepatogu ieškoti per visą failą. Todėl pridėjau | grep 1 arba perarašiau kodą į:

cat data.txt | sort | uniq -u

<img width="377" alt="Screenshot 2024-07-13 at 22 36 18" src="https://github.com/user-attachments/assets/9cd0f11d-07a8-442b-a26f-4c0c28853503">

## Level 9 > 10 

The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.

Prie galimų naudojamų komandų prisidejo strings, tad vėlgi žiūriu, ką ji gali padaryti.

Strings spausdina tekstą, o ne "heroglifus", todėl lengviau naršyti tekste.

Dabar kai jau pašalinau "heroglifus" ir žinau , kad slaptažodis yra prie kelių = simbolių, galime panaudoti
strings data.txt | grep =.

<img width="429" alt="Screenshot 2024-07-13 at 22 47 30" src="https://github.com/user-attachments/assets/b0d3f771-17a7-4e37-ae87-0ebb98a1395c">

## Level 10 > 11 

The password for the next level is stored in the file data.txt, which contains base64 encoded data

Čia puikiai atsimenu iš knygos, kaip reikia dekoduoti iš Base64, tačiau gaila, neturiu teisių kurti failų, kuriuose galėčiau išsaugoti atšifruotą kodą.

Todėl naudoju base64 -d data.txt.

<img width="424" alt="Screenshot 2024-07-13 at 22 58 03" src="https://github.com/user-attachments/assets/6d352f66-ac15-4dcf-8255-9ce56b46f392">

## Level 11 > 12 

The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

Čia tiesiog pastūmėme didžiąsias ir mažąsias raides į šoną 13 kartų.

<img width="489" alt="Screenshot 2024-07-22 at 12 07 48" src="https://github.com/user-attachments/assets/e3516733-dfd9-44a4-86d2-61f917a1ebfa">

## Level 12 > 13

The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work. Use mkdir with a hard to guess directory name. Or better, use the command “mktemp -d”. Then copy the datafile using cp, and rename it using mv

Komandas naudojau kurios skirtos failų suspaudimui, išskleidimui ir hexdump peržiūrai. Komanda xxd sukuria hexdump failo vaizdą. Komanda gzip ir bzip2 suspaudžia failus su .gz ir .bz2. Komanda tar sukuria archyvus su -cf flagu ir išskleidžia juos su -xf flagu, dažniausiai naudojama dirbant su .tar failais.

<img width="489" alt="Screenshot 2024-07-22 at 12 33 15" src="https://github.com/user-attachments/assets/2c9d7dc4-bd7b-407c-a3ce-cb05d84c318e">

## Level 13 > 14 

The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on

Prisijungiau prie bandit14 per ssh -i sshkey.private bandit14@localhost -p 2220 

Ir žinodamas kur yra pasleptas slaptažodis atidariau su cat /etc/bandit_pass/bandit14

<img width="485" alt="Screenshot 2024-07-22 at 12 45 54" src="https://github.com/user-attachments/assets/42548c7b-b024-4e95-a5b1-0ab5fe25c6c7">


## Level 14 > 15 

The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

Tiesiog prisijungiau prie localhost 30000 per telnet 

<img width="485" alt="Screenshot 2024-07-22 at 12 53 14" src="https://github.com/user-attachments/assets/48597e5e-f5dd-4812-924f-8d6223e96c55">

## Level 15 > 16

The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.
Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command…

openssl s_client -ign_eof -connect localhost:30001 prisijungiame prie serverio naudojant SSL/TLS.

<img width="496" alt="Screenshot 2024-07-22 at 15 44 36" src="https://github.com/user-attachments/assets/e87b108b-973a-4fe9-ae1b-0a29b696a0a6">

## Level 16 > 17

The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

Iš pradžių nuskenavau portus nuo 31000 iki 32000 naudodamas nmap su -sT. Gavau porą portų, prie kurių bandžiau prisijungti. Radau tinkamą portą, kur prisijungęs gavau RSA raktą. Su vim sukūriau failą sshkey.private ir įkėliau ten RSA raktą. Tada pakeičiau failo teises su chmod 600 sshkey.private ir prisijungiau prie bandit17 naudodamas ssh -i ./sshkey.private bandit17@localhost -p 2220.

<img width="488" alt="Screenshot 2024-07-22 at 16 20 57" src="https://github.com/user-attachments/assets/807d8e5b-cf6b-4bfa-a0f1-cb68e61f11b7">

## Level 17 > 18

There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new

Prie komandų, kurios gali padėti išspręsti šį lygį, pamačiau diff kuri lygina du failus, nurodydama jų skirtumus.

<img width="485" alt="Screenshot 2024-07-22 at 16 28 02" src="https://github.com/user-attachments/assets/7ad4b3d2-856f-4908-9a38-ace0ee6a918e">

## Level 18 > 19

The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.

Tiesiog ssh bandit18@bandit.labs.overthewire.org -p 2220 pridedu cat readme ir suvedu slaptazodi ir gaunu kita bandit 19 slaptazodi

<img width="485" alt="Screenshot 2024-07-22 at 17 22 58" src="https://github.com/user-attachments/assets/50017b1d-6510-46c5-aae7-bf48faa8d140">

## Level 19 > 20

To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

19 lygyje setuid naudojau, nes suteiktia teises programai, kad galėtų atidaryti ar atlikti veiksmus, kurių įprastai naudotojas negalėtų atlikti dėl leidimų apribojimų.

<img width="487" alt="Screenshot 2024-07-22 at 17 32 11" src="https://github.com/user-attachments/assets/7ad8042f-716c-469c-a2a4-8dbd2ae03d24">

## Level 20 > 21 

There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

NOTE: Try connecting to your own network daemon to see if it works as you think

Kaip supratau tai su netcatu reikia padaryti listening porta pvz 5555 ir naudoju echo kaip kad gautu sena slaptažodi. Dar pasijungiau kita terminala prisijungiau prie bandit20 ir prisijungiau prie porto su ./suconnect 5555 ir gavau slaptazodi.

<img width="629" alt="Screenshot 2024-07-24 at 13 39 35" src="https://github.com/user-attachments/assets/912b12cd-18e4-46ef-80dd-60c2cecefd1d">

## Level 21 > 22

A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

Tiesiog pasiziūrėjau kas dirba tam faile cron.d ir radau cronjob_bandit22 ko man ir reikia. Cat komanda parodo kad cron vykdo /usr/bin/cronjob_bandit22.sh . Pasižiurime  bash faila kuris sukuria failą aplanke „tmp“ ir visiems suteikia leidimą skaityti. Tada jis nukopijuoja bandit22 slaptažodžio failo įvestį į naujai sukurtą failą.

<img width="458" alt="Screenshot 2024-07-24 at 13 50 48" src="https://github.com/user-attachments/assets/65cf6b1b-1125-412a-8739-9273ae0a525c">

## Level 22 > 23

A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

NOTE: Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.

Pasižiuriu kur scriptas parasytas, atidarau ji ir matau kad galime pakeisti $myname i bandit23 ir gausime kur yra /tmp aplinkoje slaptazodis tai ir padarom ir gauname po cat komandos i /tmp/$mytarget bandit 24 slaptazodi.

<img width="459" alt="Screenshot 2024-07-24 at 14 30 11" src="https://github.com/user-attachments/assets/af7c0aa6-3a7c-4151-8f68-44478eac7f2f">

## Level 23 > 24

A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

NOTE: This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!

NOTE 2: Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…

Uztrukau ilgokai, bet sukuriau /tmp/padekdieve ir sukuriau scripta slaptikas.sh su #!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/padekdieve/slaptikas.txt

dar su chmod reikia pazaisti kad galetum vykdyti scriptus ir t.t


<img width="483" alt="Screenshot 2024-07-24 at 17 46 01" src="https://github.com/user-attachments/assets/36c6f91d-d722-4f57-83fd-0ffa9429a397">

## Level 24 > 25

A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.
You do not need to create new connections each time

Užtrukau, nes norėjau pasimokyti bash skriptinimo pradmenų. Taigi, skriptas buvo skirtas brute-force, tiesiog spėjo slaptažodį (nuo 0000 iki 9999) ir tuo pačiu metu klausėsi porto 30002.


<img width="483" alt="Screenshot 2024-07-29 at 13 04 39" src="https://github.com/user-attachments/assets/5e26633b-760a-4964-9726-26062a5c6bf4">

