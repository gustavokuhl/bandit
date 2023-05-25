# Bandit

SSH Information
Host: bandit.labs.overthewire.org
Port: 2220

## Level 0

```bash
bandit0@bandit:~$ cat readme
NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL
```

## Level 1

- Dashed filename

```bash
bandit1@bandit:~$ cat ./-
rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi
```

## Level 2

- Spaces in filename

```bash
bandit2@bandit:~$ cat spaces\ in\ this\ filename
aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG
```

## Level 3

```bash
bandit3@bandit:~$ cat inhere/.hidden
2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe
```

## Level 4

```bash
bandit4@bandit:~$ file inhere/*
inhere/-file00: data
inhere/-file01: data
inhere/-file02: data
inhere/-file03: data
inhere/-file04: data
inhere/-file05: data
inhere/-file06: data
inhere/-file07: ASCII text
inhere/-file08: data
inhere/-file09: Non-ISO extended-ASCII text, with no line terminators

bandit4@bandit:~$ cat inhere/-file07
lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR
```

## Level 5

- No tamanho especificado como "1033c", o "c" é uma unidade de medida utilizada pelo find para representar bytes exatos. Nesse contexto, "c" significa "bytes".

```bash
bandit5@bandit:~$ find inhere/ -type f -size 1033c
inhere/maybehere07/.file2
bandit5@bandit:~$ cat inhere/maybehere07/.file2
P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU
```

## Level 6

```bash
bandit6@bandit:~$ find / -user bandit7 -group bandit6 -size 33c -type f 2>/dev/null
/var/lib/dpkg/info/bandit7.password

bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S
```

## Level 7

```bash
bandit7@bandit:~$ cat data.txt | grep millionth
millionth       TESKZC0XvTetK0S9xNwm25STk5iWrBvP
```

## Level 8

```bash
bandit8@bandit:~$ cat data.txt | sort | uniq -u
EN632PlfYiZbn3PhVK3XOGSlNInNE00t
```

## Leval 9

- O comando strings no Linux é usado para extrair sequências de caracteres legíveis de arquivos, geralmente em busca de texto em arquivos binários. Ele varre um arquivo e identifica qualquer sequência de caracteres que pareça ser texto legível.

```bash
bandit9@bandit:~$ strings data.txt | grep "====="
4========== the#
========== password
========== is
========== G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s
```

## Level 10

```bash
bandit10@bandit:~$ base64 --decode data.txt
The password is 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM
```

## Level 11

- ROT13
- O comando tr é um utilitário no Linux que traduz ou exclui caracteres de entrada, substituindo-os por outros caracteres com base em duas sequências de caracteres fornecidas.

```bash
bandit11@bandit:~$ tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt
The password is JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv
```

## Level 12

- HexDump

```bash
#!/bin/bash
# descompactar.sh

# Define o arquivo que você está trabalhando
arquivo=$1

# Função para descompactar arquivos com base no tipo
descompactar() {
    local arquivo=$1

    # Determina o tipo do arquivo
    tipo=$(file -b --mime-type "$arquivo")

    # Toma a ação apropriada com base no tipo do arquivo
    case $tipo in
    application/gzip)
        mv "$arquivo" "${arquivo}.gz"
        gzip -d "${arquivo}.gz"
        descompactar "${arquivo}"
        ;;
    application/x-bzip2)
        mv "$arquivo" "${arquivo}.bz2"
        bzip2 -d "${arquivo}.bz2"
        descompactar "$arquivo"
        ;;
    application/x-tar)
        mv "$arquivo" "${arquivo}.tar"
        tar -xf "${arquivo}.tar"
        for arquivo_extraido in $(tar -tf "${arquivo}.tar"); do
            descompactar "$arquivo_extraido"
        done
        ;;
    text/plain)
        cat "$arquivo"
        ;;
    *)
        echo "Tipo de arquivo desconhecido: $tipo"
        ;;
    esac
}

descompactar $arquivo
```

```bash
bandit12@bandit:/tmp/data$ xxd -r ~/data.txt > data.bin.gz
bandit12@bandit:/tmp/data$ ./descompactar.sh data.bin.gz
The password is wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw
```
## Level 13

```bash
bandit13@bandit:~$ cat sshkey.private 
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEAxkkOE83W2cOT7IWhFc9aPaaQmQDdgzuXCv+ppZHa++buSkN+
gg0tcr7Fw8NLGa5+Uzec2rEg0WmeevB13AIoYp0MZyETq46t+jk9puNwZwIt9XgB
ZufGtZEwWbFWw/vVLNwOXBe4UWStGRWzgPpEeSv5Tb1VjLZIBdGphTIK22Amz6Zb
ThMsiMnyJafEwJ/T8PQO3myS91vUHEuoOMAzoUID4kN0MEZ3+XahyK0HJVq68KsV
ObefXG1vvA3GAJ29kxJaqvRfgYnqZryWN7w3CHjNU4c/2Jkp+n8L0SnxaNA+WYA7
jiPyTF0is8uzMlYQ4l1Lzh/8/MpvhCQF8r22dwIDAQABAoIBAQC6dWBjhyEOzjeA
J3j/RWmap9M5zfJ/wb2bfidNpwbB8rsJ4sZIDZQ7XuIh4LfygoAQSS+bBw3RXvzE
pvJt3SmU8hIDuLsCjL1VnBY5pY7Bju8g8aR/3FyjyNAqx/TLfzlLYfOu7i9Jet67
xAh0tONG/u8FB5I3LAI2Vp6OviwvdWeC4nOxCthldpuPKNLA8rmMMVRTKQ+7T2VS
nXmwYckKUcUgzoVSpiNZaS0zUDypdpy2+tRH3MQa5kqN1YKjvF8RC47woOYCktsD
o3FFpGNFec9Taa3Msy+DfQQhHKZFKIL3bJDONtmrVvtYK40/yeU4aZ/HA2DQzwhe
ol1AfiEhAoGBAOnVjosBkm7sblK+n4IEwPxs8sOmhPnTDUy5WGrpSCrXOmsVIBUf
laL3ZGLx3xCIwtCnEucB9DvN2HZkupc/h6hTKUYLqXuyLD8njTrbRhLgbC9QrKrS
M1F2fSTxVqPtZDlDMwjNR04xHA/fKh8bXXyTMqOHNJTHHNhbh3McdURjAoGBANkU
1hqfnw7+aXncJ9bjysr1ZWbqOE5Nd8AFgfwaKuGTTVX2NsUQnCMWdOp+wFak40JH
PKWkJNdBG+ex0H9JNQsTK3X5PBMAS8AfX0GrKeuwKWA6erytVTqjOfLYcdp5+z9s
8DtVCxDuVsM+i4X8UqIGOlvGbtKEVokHPFXP1q/dAoGAcHg5YX7WEehCgCYTzpO+
xysX8ScM2qS6xuZ3MqUWAxUWkh7NGZvhe0sGy9iOdANzwKw7mUUFViaCMR/t54W1
GC83sOs3D7n5Mj8x3NdO8xFit7dT9a245TvaoYQ7KgmqpSg/ScKCw4c3eiLava+J
3btnJeSIU+8ZXq9XjPRpKwUCgYA7z6LiOQKxNeXH3qHXcnHok855maUj5fJNpPbY
iDkyZ8ySF8GlcFsky8Yw6fWCqfG3zDrohJ5l9JmEsBh7SadkwsZhvecQcS9t4vby
9/8X4jS0P8ibfcKS4nBP+dT81kkkg5Z5MohXBORA7VWx+ACohcDEkprsQ+w32xeD
qT1EvQKBgQDKm8ws2ByvSUVs9GjTilCajFqLJ0eVYzRPaY6f++Gv/UVfAPV4c+S0
kAWpXbv5tbkkzbS0eaLPTKgLzavXtQoTtKwrjpolHKIHUz6Wu+n4abfAIRFubOdN
/+aLoRQ0yBDRbdXMsZN/jvY44eM+xRLdRVyMmdPtP8belRi2E2aEzA==
-----END RSA PRIVATE KEY-----
```

## Level 14
