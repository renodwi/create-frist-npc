# Membuat npc pertama
kali ini saya bakal menjelaskan cara ngebikin npc di SA:MP pakai bahasa indonesia, berikut langkah langkah nya <br> <br>

[**DOWNLOAD SCRIPT RECORDING NYA DI SINI**](https://github.com/Southclaws/samp-Hellfire/blob/master/filterscripts/npc_record.pwn)
## Recording a playback file
Pertama-tama, kita perlu merekam file pemutaran untuk digunakan NPC kita. Sebelum kita memulai merekam file untuk npc kita, kita perlu memasang filterscript
[npc record](https://github.com/Southclaws/samp-Hellfire/blob/master/filterscripts/npc_record.pwn) agar dapat memulai perekaman npc. Setelah filterscript
tersebut terpasang, lalu masuk rcon (ketik "/rcon login <password rcon>") dan muat filterscript (ketik "/rcon loadfs npc_record"). Sekarang ada 3 perintah dalam filterscript npc_record

- **/vrecord <filename> Mulai merekam jalur kendaraan ke nama file yang ditentukan.**
- **/ofrecord <filename> Mulai merekam jalur jalan kaki ke nama file yang ditentukan.**
- **/stoprecord Berhenti merekam kendaraan dan jalur pejalan kaki.**

Dalam tutorial ini, kita akan membuat rekaman jalur kendaraan, jadi masuk ke dalam kendaraan, dan ketik /vrecord npcku (Anda harus login ke rcon) untuk mulai merekam.
lalu berkelilinglah sebentar dan ketika Anda selesai ketik /stoprecord.

Tutup game, dan pergi ke direktori scriptfiles gamemode Anda, seharusnya ada file bernama npcku.rec. pindahkan file tersebut kedalam <gamemodemu/npcmodes/recordings/>.

## Mengontrol NPC
Ini adalah skrip simple yang akan mengontrol pergerakan npc anda.
```
#define RECORDING "npcku" // Ini adalah nama file rekaman.
#define RECORDING_TYPE 1 // 1 untuk rekaman kendaraan, 2 untuk remakan jalan kaki (onfoot).

#include <a_npc>
main(){}
public OnRecordingPlaybackEnd() StartRecordingPlayback(RECORDING_TYPE, RECORDING);

#if RECORDING_TYPE == 1
  public OnNPCEnterVehicle(vehicleid, seatid) StartRecordingPlayback(RECORDING_TYPE, RECORDING);
  public OnNPCExitVehicle() StopRecordingPlayback();
#else
  public OnNPCSpawn() StartRecordingPlayback(RECORDING_TYPE, RECORDING);
#endif
```
Compline skrip tersebut lalu simpan di <gamemodemu/npcmodes> ( saya simpan menggunakan nama npcku.pwn )

## Mengkoneksikan NPC ke server
Sekarang kita akan mengkoneksikan NPC kedalam server.
```
ConnectNPC("RenChan","npcku");
```
- **RenChan** adalah nama untuk NPC yang akan terkoneksi kedalam server
- **npcku** adalah nama file pengontrol NPC

Mari kita coba menghubungkan npc saat gamemode termuat.
```
public OnGameModeInit()
{
  print("Hello World!");
  ConnectNPC("RenChan","npcku");
  return 1;
}
```
Sekarang kita akan membuat kendaraan untuk NPC.
**_Catatan : Jika npc anda tidak menggunakan kendaraan, anda dapat melewati ini_**
```
new RenChanNPCVehicle; //Global variable!
public OnGameModeInit()
{
  print("Hello World!");
  ConnectNPC("RenChan","npcku");
  RenChanNPCVehicle = CreateVehicle(400, 0.0, 0.0, 5.0, 0.0, 3, 3, 5000);
  return 1;
}
```
Perhatikan bahwa lokasi sebenarnya kendaraan tidak masalah, karena akan diteleportasi ke mana pun jalur NPC dimulai, saat jalur mulai diputar.

Hanya satu hal lagi sebelum Anda dapat masuk ke dalam game dan menguji NPC pertama Anda, anda harus memasukkan NPC ke dalam kendaraan yang anda buat untuk itu.
Saya melakukan ini menggunakan OnPlayerSpawn..
```
public OnPlayerSpawn(playerid)
{
  if(IsPlayerNPC(playerid)) // Untuk mengecek bahwa itu adalah npc
  {
    new npcname[MAX_PLAYER_NAME];
    GetPlayerName(playerid, npcname, sizeof(npcname)); // Mengambil nama npc
    if(!strcmp(npcname, "RenChan", true)) // Mengecek bahawa npc tersebut bernama "RenChan"
    {
      PutPlayerInVehicle(playerid, RenChanNPCVehicle, 0); // Memasukan npc kedalam kendaraan yang telah dibuat.
    }
    return 1;
  }
  // hal hal lain untuk player normal berada di sini
  return 1;
}
```
Sekarang compline gamemode anda dan coba lah.
## Beberapa masalah yang sering terjadi
- **NPC saya meninggalkan server saya setelah terkoneksi.**
<br>Script Anda memaksa NPC untuk login, atau Anda memiliki penendang anti-cheat / ping yang mengganggu NPC Anda. Kamu bisa menambahkan skrip ini di beberapa skrip gamemode anda
```
if(IsPlayerNPC(playerid)) return 1;
```
- **NPC saya tidak bergabung dengan server saya sama sekali.**
<br>Ini kemungkinan besar disebabkan oleh server Anda yang di-password
- **NPC saya hanya berdiri di spawnpoint**
<br>Baca kembali, dan lakukan kembali bagian OnPlayerSpawn dari tutorial.

**_Catatan : anda harus mengubah maksimal jumlah npc yang dapat terkoneksi kedalam server dibagian server.cfg_**


