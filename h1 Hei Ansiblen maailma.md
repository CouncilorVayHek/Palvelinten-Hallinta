# x) Lue ja tiivistä

## Karvinen 2026: SSH public key - Login without password
- SSH on turvallinen tapa kirjautua palvelimelle etänä.
- OpenSSH-palvelin asennetaan ja käynnistetään palveluna.
- Yhteys testataan komennolla `ssh localhost`.
- Julkisen avaimen tunnistautuminen tehdään komennoilla `ssh-keygen` ja `ssh-copy-id`.
- Tämän jälkeen kirjautuminen onnistuu ilman salasanan syöttämistä.
- Vianmääritykseen sopivat esimerkiksi `ssh -v` ja `systemctl status ssh`.

Lähde: https://terokarvinen.com/hello-ansible/

## Karvinen 2026: Hello Ansible
- Ansible on konfiguraationhallintatyökalu, jolla hallitaan koneita koodilla.
- Se toimii SSH:n yli eikä tarvitse agenttia kohdekoneelle.
- Kohdekoneella tarvitaan SSH ja Python.
- Ansiblella voidaan suorittaa komentoja etänä ja ajaa playbookeja.
- Yleisiä virheitä ovat puuttuva inventaario, Python-varoitukset ja YAML-sisennysvirheet.

Lähde: https://terokarvinen.com/hello-ansible/

# a) Sshecrets
- Asenna SSH-palvelin:
  ```
  sudo apt-get update
  sudo apt-get -y install ssh
  sudo systemctl enable --now ssh
  ```
Testaa yhteys käyttämällä ssh localhost ja yhteyden luotua poistu exit -komennolla.


# b) Pubkey


Luo avainpari:
  ```ssh-keygen  ```
  
Kopioi julkinen avain:
  ```ssh-copy-id localhost ```
  
Testaa kirjautuminen:
  ```ssh localhost ```

# c) Hei Ansible
Asenna Ansible:
```sudo apt-get update
sudo apt-get install ansible micro bash-completion tree
```

Luo kansio ja siirry sinne:
```
mkdir ansibles
cd ansibles
```

Luo hosts.ini:
```
[web]
xxx@localhost
```
Luo site.yml:
```
- hosts: all
  roles:
    - hello
```
Luo roles/hello/tasks/main.yml:
```
- copy:
    dest: /tmp/hello-ansible
    content: "Heippa, ansiblen maailma!\n"
```
Aja ohjelma:
```
ansible-playbook site.yml -i hosts.ini --ask-become-pass
```



<img width="1073" height="499" alt="kuva" src="https://github.com/user-attachments/assets/6bbdf82e-813f-4f56-90ed-92870c0dccc7" />
