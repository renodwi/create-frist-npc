# Membuat npc pertama
kali ini saya bakal menjelaskan cara ngebikin npc di SA:MP pakai bahasa indonesia, berikut langkah langkah nya

## Recording a playback file
Pertama-tama, kita perlu merekam file pemutaran untuk digunakan NPC kita. Sebelum kita memulai merekam file untuk npc kita, kita perlu memasang filterscript
[npc record](https://github.com/Southclaws/samp-Hellfire/blob/master/filterscripts/npc_record.pwn) agar dapat memulai perekaman npc. Setelah filterscript
tersebut terpasang, lalu masuk rcon (ketik "/rcon login <password rcon>") dan muat filterscript (ketik "/rcon loadfs npc_record"). Sekarang ada 3 perintah dalam filterscript npc_record

- **/vrecord <filename> Mulai merekam jalur kendaraan ke nama file yang ditentukan.**
- **/ofrecord <filename> Mulai merekam jalur jalan kaki ke nama file yang ditentukan.**
- **/stoprecord Berhenti merekam kendaraan dan jalur pejalan kaki.**

Dalam tutorial ini, kita akan membuat rekaman jalur kendaraan, jadi masuk ke dalam kendaraan, dan ketik /vrecord npcku (Catatan Anda harus login ke rcon) untuk mulai merekam.
lalu berkelilinglah sebentar dan ketika Anda selesai ketik /stoprecord.

Tutup game, dan pergi ke direktori scriptfiles gamemode Anda, seharusnya ada file bernama npcku.rec. pindahkan file tersebut kedalam <gamemodemu/npcmodes/recordings/>.
