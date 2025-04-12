# Praktikum-6-M.Rifky-Erlangga
E.Tugas Praktikum 6
1. Melihat Daftar Proses
Jalankan perintah berikut:
'''bash
ps -au
a. Nama proses bukan root: Contoh output:
studentOS  3174  0.0  bash
studentOS  3181  0.1  ps

b. Proses dengan CPU Time tertinggi:
PID     COMMAND
1502    firefox

c. Buyut proses dari proses tersebut:
pstree -sp 1502
systemd(1)───gnome-terminal(1123)───bash(1400)───firefox(1502)

d. Beberapa proses daemon:
- systemd
- dbus-daemon
- cron
- cupsd

e. Percobaan prompt shell:
$ csh
$ sh
$ bash
$ ls
$ ps

2. Uji Program prog.sh
Script:
#!/bin/sh
trap "echo Hello Goodbye ; exit 0" 1 2 3 15
echo "Program berjalan ~"
while :
do
  echo "X"
  sleep 20
done

Jalankan di background:
chmod +x prog.sh
./prog.sh &

Coba hentikan dengan berbagai sinyal:
kill -1 [PID]
kill -2 [PID]
kill -3 [PID]
kill -15 [PID]

Hasil:
Proses berhenti saat dikirim sinyal 15 (SIGTERM) dan menampilkan Hello Goodbye.

3. Modifikasi Script myjob.sh
Script:
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

Penjelasan:
Script akan mencari semua file dan direktori dari root (/), menyimpan dan mengurutkannya.
Proses berjalan di background.
Setelah 60 detik, proses dihentikan dengan kill -15, dan akan mencetak pesan Proses dihentikan dari trap
