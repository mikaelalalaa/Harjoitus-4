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


![image](https://user-images.githubusercontent.com/93308960/143080898-c53388ab-23d8-46e5-8e93-d9e930c7978a.png)


![image](https://user-images.githubusercontent.com/93308960/143081754-935aba59-55ab-4333-b3f0-4e6a7ab11186.png)

![image](https://user-images.githubusercontent.com/93308960/143081654-90d98326-e7a9-4a4b-a207-a3d6abfa2159.png)

![image](https://user-images.githubusercontent.com/93308960/143083129-23272a19-ed7c-46b8-8949-c31bdb8a3af6.png)



![image](https://user-images.githubusercontent.com/93308960/143070879-86dc076a-2e5d-47a2-b6dd-d0fe09b130d7.png)



## d) Asenna jokin toinen ohjelma asetuksineen.

![image](https://user-images.githubusercontent.com/93308960/143084715-4407d45b-306b-40b3-9555-10b4560874fb.png)



![image](https://user-images.githubusercontent.com/93308960/143084780-69130426-e897-45db-ae5b-41f56d647052.png)


![image](https://user-images.githubusercontent.com/93308960/143084658-4a74ce84-b227-46df-aa14-2bbfb5ffe0e3.png)

