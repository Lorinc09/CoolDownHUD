# CoolDownHUD

Este, játék után megmutatja, mikor hűlt le a géped annyira, hogy nyugodtan kikapcsolhasd — és ha
mégis meleg géppel akarod leállítani, előbb rákérdez.

Amikor kikapcsolod a gépet, a ventilátorok azonnal leállnak. Ha a hűtőbordában még benne van a
játék melege, az visszaszivárog az alkatrészekbe — ez hosszú távon nem tesz jót nekik. Ez a program
megmondja, mikor van túl ezen a gép.

## Mit csinál

- Figyeli a processzor és a videokártya hőmérsékletét.
- **Este 8-tól**, amikor már nem fut semmi terhelés, megjelenít egy kis kijelzőt a képernyő jobb
  felső sarkában.
- Csak akkor vált zöldre (`CLEAR TO POWER OFF`), ha a hőfokok **két percen át folyamatosan** hidegek
  maradtak. Ha közben visszamelegszik, a számláló újraindul.
- Amikor zöldre vált, egyszer megszólal egy halk hang.
- Ha egy ablak eltakarná, átugrik a másik monitorra. Ha nincs hova, elrejtőzik, és visszajön, amint
  felszabadul a hely.
- Játék közben nem látszik.
- **Ha meleg géppel indítasz leállítást, megkérdezi, biztos vagy-e benne.** Ez egész nap érvényes,
  nem csak este.

**Nem kell beállítani semmit.** A program az első használat során megtanulja, milyen a te géped
nyugalomban, és ahhoz méri magát. Amíg tanul, `CALIBRATING` felirat látszik rajta.

## Mi kell hozzá

Windows 10 vagy 11, 64 bites. Ezen felül semmit nem kell előre feltelepíteni: a program mindent
hoz magával.

A hőfokokat több forrásból is ki tudja olvasni. Az első indításkor mindet végigpróbálja, a legjobbat
választja, és egy ablakban megmutatja, mit talált:

| Forrás | Mit ad | Mikor működik |
|---|---|---|
| GIGABYTE SIV | processzor | GIGABYTE alaplap, telepített APP Center / SIV |
| Beépített szenzorkönyvtár | processzor és videokártya | mindenhol; a processzorhoz kell hozzá a PawnIO driver |
| HWiNFO | processzor és videokártya | ha fut a HWiNFO, bekapcsolt „Shared Memory Support" mellett |
| LibreHardwareMonitor / OpenHardwareMonitor | processzor és videokártya | ha fut valamelyik program |
| NVIDIA meghajtó | videokártya | NVIDIA kártya, telepített meghajtóval |
| ACPI hőzóna | processzor (közelítés) | a legtöbb gépen, de nem mindig a procimagot méri |

### Ha nincs processzor-hőmérséklet

A processzor maghőfokját Windows alatt csak kernel szintről lehet kiolvasni. Ha a fenti források
egyike sem érhető el, a program felajánlja a **PawnIO** telepítését — ez egy önálló, nyílt forrású,
digitálisan aláírt driver, ami ezt a hozzáférést biztosítja. Egy gombnyomás; a telepítő a saját
kiadási oldaláról töltődik le, és a program futtatás előtt ellenőrzi az aláírását.

Ez a te döntésed: a program nem telepít drivert a hátad mögött. Nélküle is elindul, csak a
processzor hőfokát nem fogja látni.

## Telepítés

1. Töltsd le a telepítőt:
   **[CoolDownHUD-Setup.exe](https://github.com/Lorinc09/CoolDownHUD/releases/latest/download/CoolDownHUD-Setup.exe)**
   — ez a cím mindig a legfrissebb verziót adja.
2. Indítsd el.

### A Windows figyelmeztetni fog

A telepítő nincs digitálisan aláírva (egy tanúsítvány évi több száz euró), ezért a Windows
SmartScreen kék ablakot mutat:

> **A Windows megvédte a gépét**

Ilyenkor kattints a **További információk** feliratra, majd a megjelenő **Futtatás mindenképp**
gombra. Ez nem hiba, és nem jelenti azt, hogy a fájllal baj van — csak annyit, hogy a Microsoft nem
ismeri a kiadóját.

A telepítés rendszergazda jóváhagyást kér. Erre azért van szükség, mert a processzor
maghőmérsékletét a Windows csak emelt joggal engedi kiolvasni.

## Használat

A program a tálcán ül, a színes pötty mutatja az állapotot:

| Szín | Jelentés |
|---|---|
| szürke | figyel, vagy terhelés alatt van a gép |
| narancs | hűl, még nem kapcsolható ki |
| zöld | kikapcsolható |

Vidd rá az egeret: megjelenik a két hőfok és a hozzájuk tartozó határ. Jobb gombbal egy rövid menü
nyílik: a kijelző elrejtése, a hangjelzés kapcsolója és a kilépés.

A kijelzőt **Alt + bal gombbal** lehet áthelyezni, ha máshol szeretnéd.

## A leállítás előtti kérdés

Ha a gép még meleg, és leállítod, a program közbelép, és megmutatja a két hőfokot a hozzájuk tartozó
határral. Két választásod van: `Keep cooling` (marad bekapcsolva) vagy `Power off anyway` (leáll).
Az Enter és az Esc is a biztonságos választ adja.

Néhány dolgot érdemes tudni róla, mert ezek a Windows korlátai, nem a programéi:

- **A Windows a saját kék lapját is kirakja** a leállítást akadályozó programokról. Ezt nem lehet
  elnyomni; a CoolDownHUD szövege ezen a lapon is ott áll. Ha a *Mégse* gombot választod, alatta
  megtalálod a program saját ablakát a valódi gombokkal.
- **Újraindításkor is kérdezni fog**, pedig ott a ventilátorok végig járnak: a Windows nem árulja
  el, hogy leállításról vagy újraindításról van-e szó. A kijelentkezést viszont felismeri, és
  kihagyja.
- **Alvó állapotra és hibernálásra nem kérdez rá.** Azokat a Windows nem kérdésként, hanem
  értesítésként küldi — nincs mód megállítani őket.
- **Kényszerített leállításnál** (`shutdown /f`, rendszerfrissítés határideje, lemerülő akkumulátor)
  szándékosan nem akadékoskodik.

## Frissítés

A program naponta egyszer megnézi, van-e újabb verzió, és ha van, magától letölti és telepíti.
Nem kell vele foglalkoznod. Játék közben soha nem frissít.

## Eltávolítás

A Windows *Beállítások → Alkalmazások* listájából, mint bármely más programot.

## Felhasznált munkák

- [LibreHardwareMonitor](https://github.com/LibreHardwareMonitor/LibreHardwareMonitor) — MPL-2.0.
  A licencszöveg a telepítési mappa `licenses` almappájában található.
- [PawnIO](https://pawnio.eu) — GPL-2.0. Nem része a telepítőnek; a program csak felajánlja, és a
  saját kiadási oldaláról tölti le, ha kéred.
