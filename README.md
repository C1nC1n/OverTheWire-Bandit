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

Atidarius data.txt pasipyle daug vardu ir slaptazodziu tai tiesiog atrinkti millionth naudojau grep komanda

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

Komandas naudojau kurios skirtos failų suspaudimui, išskleidimui ir hexdump peržiūrai. Komanda xxd sukuria hexdump failo vaizdą arba atkuria failą iš hexdump. Komanda gzip ir bzip2 suspaudžia failus arba išskleidžia juos su -d taikomos failams su .gz ir .bz2 plėtiniais. Komanda tar sukuria archyvus su -cf flagu ir išskleidžia juos su -xf flagu, dažniausiai naudojama dirbant su .tar failais.

<img width="489" alt="Screenshot 2024-07-22 at 12 33 15" src="https://github.com/user-attachments/assets/2c9d7dc4-bd7b-407c-a3ce-cb05d84c318e">

## Level 13 > 14 

The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on

Prisijungiau prie bandit14 per ssh -i sshkey.private bandit14@localhost -p 2220 

Ir zinodemas kur yra pasleptas slaptazodis atidariau su cat /etc/bandit_pass/bandit14

<img width="485" alt="Screenshot 2024-07-22 at 12 45 54" src="https://github.com/user-attachments/assets/42548c7b-b024-4e95-a5b1-0ab5fe25c6c7">


## Level 14 > 15 

