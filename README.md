**hapus Docker lama → install Docker versi 28.1.0-1** di Debian 13 (Trixie):


## **1. Hapus semua Docker versi sebelumnya**

```
systemctl stop docker
systemctl stop containerd

apt remove -y docker docker.io docker-engine docker-ce docker-ce-cli containerd.io
apt purge -y docker* containerd*
apt autoremove -y

rm -rf /var/lib/docker
rm -rf /var/lib/containerd
```

---

## **2. Tambahkan repository Docker resmi (untuk Debian TRIXIE)**

```
apt update
apt install -y ca-certificates curl gnupg

install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.gpg
chmod a+r /etc/apt/keyrings/docker.gpg
```

Tambahkan ke sources.list:

```
echo "deb [arch=arm64 signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
$(. /etc/os-release; echo $VERSION_CODENAME) stable" \
| tee /etc/apt/sources.list.d/docker.list > /dev/null

apt update
```

---

## **3. Install Docker versi 28.1.0-1**

```
apt install -y docker-ce=5:28.1.0-1~debian.13~trixie \
               docker-ce-cli=5:28.1.0-1~debian.13~trixie \
               containerd.io
```

(atau `containerd` jika containerd.io tidak tersedia)

---

## **4. Cek instalasi**

```
docker --version
```

Output yang benar:

```
Docker version 28.1.0, build ...
```
