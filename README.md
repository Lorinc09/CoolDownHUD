# CoolDownHUD

Este, játék után megmutatja, mikor hűlt le a géped annyira, hogy nyugodtan kikapcsolhasd.

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

**Nem kell beállítani semmit.** A program az első használat során megtanulja, milyen a te géped
nyugalomban, és ahhoz méri magát. Amíg tanul, `CALIBRATING` felirat látszik rajta.

## Mi kell hozzá

| | |
|---|---|
| Windows | 10 vagy 11 (64 bites) |
| Processzor hőfokához | **GIGABYTE alaplap**, telepített GIGABYTE APP Center / SIV programmal |
| Videokártya hőfokához | **NVIDIA** kártya, telepített meghajtóval |

Más gépeken a program elindul, de nem tud hőfokot mérni — ilyenkor ezt ki is írja a kijelzőn.
Semmi mást nem kell előre feltelepíteni: a program mindent hoz magával.

## Telepítés

1. Töltsd le a legfrissebb `CoolDownHUD-Setup-x.y.z.exe` fájlt a
   [kiadások](../../releases/latest) közül.
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

## Frissítés

A program naponta egyszer megnézi, van-e újabb verzió, és ha van, magától letölti és telepíti.
Nem kell vele foglalkoznod. Játék közben soha nem frissít.

## Eltávolítás

A Windows *Beállítások → Alkalmazások* listájából, mint bármely más programot.
