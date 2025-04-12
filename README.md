### 1. Melihat Daftar Proses

Jalankan perintah berikut:
```bash
ps -au
```

**a. Nama proses bukan root:**
Contoh output:
```
studentOS  3174  0.0  bash
studentOS  3181  0.1  ps
```

**b. Proses dengan CPU Time tertinggi:**
```
PID     COMMAND
1502    firefox
```

**c. Buyut proses dari proses tersebut:**
```bash
pstree -sp 1502
systemd(1)───gnome-terminal(1123)───bash(1400)───firefox(1502)
```

**d. Beberapa proses daemon:**
- `systemd`
- `dbus-daemon`
- `cron`
- `cupsd`

**e. Percobaan prompt shell:**
```bash
$ csh
$ sh
$ bash
$ ls
$ ps
```

---

### 2. Uji Program `prog.sh`

**Script:**
```bash
#!/bin/sh
trap "echo Hello Goodbye ; exit 0" 1 2 3 15
echo "Program berjalan ~"
while :
do
  echo "X"
  sleep 20
done
```

**Jalankan di background:**
```bash
chmod +x prog.sh
./prog.sh &
```

**Coba hentikan dengan berbagai sinyal:**
```bash
kill -1 [PID]
kill -2 [PID]
kill -3 [PID]
kill -15 [PID]
```

**Hasil:**
- Proses berhenti saat dikirim sinyal **15 (SIGTERM)** dan menampilkan `Hello Goodbye`.

---

### 3. Modifikasi Script `myjob.sh`

**Script:**
```bash
#!/bin/sh
trap "echo 'Proses dihentikan'; exit 0" 15
i=1
while :
do
  find / -print > berkas
  sort berkas > hasil
  echo "Proses selesai pada $(date)" >> proses.log
  sleep 60
  i=$((i+1))
done &
PID=$!
sleep 60
kill -15 $PID
```

