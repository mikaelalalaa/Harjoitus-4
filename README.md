# Harjoitus-4


Tehtävät löytyvät opettajamme [Tero Karvisen sivulta](https://terokarvinen.com/2021/configuration-management-systems-palvelinten-hallinta-ict4tn022-2021-autumn/#h4-aikajana)

## a) Captain obvious

Aluksi ladattiin saltin avulla 10 eri ohjelmaa. Ensin tein tiedoston `init.sls` `srv/salt/tenfave` hakemistoon.

Ohjelmoiksi valitsin

 * apache 
 * openssh-server
 * mysql-server
 * net-tools
 * nmap
 * micro
 * gimp
 * vim
 * tree
 * filezillan

![image](https://user-images.githubusercontent.com/93308960/143049544-41f4bef5-356a-41cd-ab7c-5ed5c1282c9a.png)

Tämän jälkeen tallensin tiedoston ja ajoin komennon

```
sudo salt-call --local -l info state.apply tenfave
```

![image](https://user-images.githubusercontent.com/93308960/143049655-f687b1e3-446f-4489-9819-01e3b607a56a.png)

Kuten tuloksesta huomaa 6 ohjelmaa oli asennettu jo ja neljä ohjelmaa (micro, net-tools, tree ja vim) saatii onnistuneestin asennettua.


## b) CSI Pasila

Ajoin aikajana komennon ja alla olevassa kuvassa näkyy muutokset joita ollaan tehty `etc` hakemistossa.

```
cd /etc/; sudo find -printf '%T+ %p\n'|sort|tail
```
![image](https://user-images.githubusercontent.com/93308960/143049938-f715fc53-a304-4359-a70d-e57ac5b61433.png)

Komennon tarkoitus:

* **cd /etc/;** tarkoittaa mistä hakemistosta aikajanaa haetaan
* **sudo find** tarkoittaa että komento ajetaan sudo oikeuksilla eli pääkäyttäjä 
* **-prinff** tarkentaa mitä asiaoita komento esittää
* **%T+** kertoo tiedoston muokkauksen ajan ja päivän
* **%p** kertoo tiedoston nimen
* **\n** tekee rivinvaihdon
* **sort** järjestää tulokset
* **tail** tulostaa 10 viimeistä

Ennen kun ajoin uudestaan aikajana komennon tein pieniä muutoksia. 

Tein "reijän" palomuuriin mysql. Komento oli `sudo ufw allow mysql`.

Sitten ajoin aikajanan komenmnon uudestaan ja kuten kuvassa näkyy että muutokset tuli voimaan. 

![image](https://user-images.githubusercontent.com/93308960/143051736-c5418d3a-624e-4b62-9de9-ea9a9932eb51.png)



## c) Tiedän mitä teit viime kesän

Tein tyyli muutoksia nano tiedostooni. Kirjoitin alla olevan tekstin `.nanorc` tiedostoon

```
## configure file

set linenumbers
set titlecolor yellow,black
set numbercolor yellow
set keycolor magenta
```

Tämän jälkeen tein aikajana komennon jossa näky että tiedostolle `.nanorc` on tehty muutoksia

![image](https://user-images.githubusercontent.com/93308960/143080898-c53388ab-23d8-46e5-8e93-d9e930c7978a.png)

Tämän jälkeen poistin nano ohjelman komennolla `sudo apt remove nano`.

Sitten tein hakemiston `srv/salt/nanno` ja loin teksti tiedoston `init.sls`.

Johon laitoin alla olevan tekstin:

```
nano:
  pkg.installed

/home/roott/:
  file.directory:
    - source: /home/roott/
    - user: roott
    - mode: 700

/home/roott/.nanorc:
  file.managed:
    - source: /home/roott/.nanorc
    - user: roott
    - mode: 700

```

Ajoin komennon 

```
sudo salt-call --local -l info state.apply nanno
```

Kuten kuvasta näkyy asennus ja muutokset onnistuivat.

![image](https://user-images.githubusercontent.com/93308960/143070879-86dc076a-2e5d-47a2-b6dd-d0fe09b130d7.png)

Tämän jälkeen kävin vielä katsomassa tyyli muutokset, tulivat voimaan poiston jälkeen.

Kuvassa näkyy että tuli voimaan.

![image](https://user-images.githubusercontent.com/93308960/143091237-979ba7c5-d18f-4280-928a-4159d607fe9b.png)


## d) Asenna jokin toinen ohjelma asetuksineen.

Jotta pystyisin tehdä suunnittelemani mukaan, poistin apache2 komennolla `sudo apt-get autoremove apache2`.


Eli aloitin taas tekemmällä hakemiston `srv/salt/apacete` sinne loin taas `init.sls` tiedoston.

Ensiksi laitoin koodiski alla olevan tekstin 

```
apache2:
  pkg.installed:
      - pkgs: 
        - apache 2
  
testi  
  file.managed:
      - name: /etc/apache2/sites-available
      - mode: insert
      - content: "portti 80"
```

Tallensin ja ajoin komennon 

```
sudo salt-call --local -l info state.apply apacete
```

Noh niinkuin alla olevasta kuvasta näkyy apache2 asennus onnistui mutta se file.managed ei onnistunut.

![image](https://user-images.githubusercontent.com/93308960/143084715-4407d45b-306b-40b3-9555-10b4560874fb.png)

Joten päätimpä muokata `init.sls` tiedostoani.

Kirjoitin tiedostoon alla olevan tekstin.

```
apache2:
  pkg.installed:
      - pkgs: 
        - apache 2
  
test  
  cmd.run:
    - name: ufw allow apache    
```

ajoin saman komennon uudestaan *`sudo salt-call --local -l info state.apply apacete`*

Alla olevasta kuvasta näkyy että muutokset onnistui.

![image](https://user-images.githubusercontent.com/93308960/143084658-4a74ce84-b227-46df-aa14-2bbfb5ffe0e3.png)

