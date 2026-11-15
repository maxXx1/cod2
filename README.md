# Bitcore.cz — CoD2x zPAM 4.12 Competitive Deathmatch Server

Český veřejný Deathmatch (aim warmup) server pro **Call of Duty 2** běžící na komunitním patchi **CoD2x** a competitive módu **zPAM 4.12**.

- **Část 1:** [Pro hráče — Jak se připojit a co čekat na serveru](#část-1-pro-hráče--jak-se-připojit-a-co-čekat-na-serveru)
- **Část 2:** [Pro administrátory — Konfigurace a nasazení serveru](#část-2-pro-administrátory--konfigurace-a-nasazení-serveru)

---

## Část 1: Pro hráče — Jak se připojit a co čekat na serveru

### Co potřebuješ ke hraní (stažení klienta)

1. **Základní hru Call of Duty 2** (verze `1.3`).
2. **Klient CoD2x (`v1.4.6.8` nebo novější):**
   Server běží na protokolu CoD2x (`1.4`), takže bez klientského patche CoD2x se nepřipojíš.
   - **Oficiální stránka vydání:** https://github.com/callofduty2x/CoD2x/releases/tag/v1.4.6.8
   - **Přímé stažení pro Windows:** [`CoD2x_1.4.6.8_windows.zip`](https://github.com/callofduty2x/CoD2x/releases/download/v1.4.6.8/CoD2x_1.4.6.8_windows.zip)
   - **Domovský repozitář projektu:** https://github.com/callofduty2x/CoD2x
3. **Mód zPAM `4.12` a `_fix` mapy (`zpam_maps_v7.iwd`):**
   - Chybějící soubory (`zpam412.iwd` ~6,4 MB a `zpam_maps_v7.iwd` ~178 MB) se Ti **stáhnou automaticky** při připojení přes FastDL (`http://cod2x.me/zpam`).
   - Ujisti se, že máš v konzoli povolené stahování: `/cl_allowDownload 1` a `/cl_wwwDownload 1`.
   - Pokud si chceš balík stáhnout předem ručně, rozbal do složky `Call of Duty 2/main/` soubory `.iwd` z oficiálního archivu: [`zpam412.zip`](https://github.com/eyza-cod2/zpam3/releases/download/4.12/zpam412.zip) ([přehled verzí](https://github.com/eyza-cod2/zpam3/releases)).

> **Tip pro nalezení v prohlížeči serverů:** Server je označen jako **Pure: Yes** (`sv_pure 1`) a **Mod: Yes**. Ve výchozím filtru CoD2 (`Pure: Yes`, `Mod: All`) ho uvidíš normálně; pouze pokud máš ručně zapnutý filtr `Mod: No`, přepni ho na `All`.

---

### Jaké nastavení a pravidla tě na serveru čekají

Server je zaměřený na **čistý aim trénink a rozehřátí před zápasy** (max. **10 hráčů**):

- **Plynulý Deathmatch:** okamžitý start bez čekání na ready-up (`F4`), bez úvodního odpočtu, bez killcamy a bez automatického nahrávání dema.
- **Konec mapy:** mapa se přepne na další v rotaci po **30 minutách** nebo jakmile první hráč dosáhne **50 killů**.
- **Výběr zbraní bez spamu:** všechny pušky, samopaly (SMG), sniperky i kulomety jsou povolené. **Frag granáty, smoke granáty a brokovnice jsou vypnuté** (ani nepadají po smrti).
- **Competitive chování hry (`g_competitive 1` + zPAM 4.12):**
  - Klientu se automaticky srovnají síťové a FPS limity na soutěžní hodnoty: `com_maxfps` `125–250`, `rate 25000`, `snaps 40`, `cl_maxpackets 125`, vypnuté dynamické stíny (`sc_enable 0`), `fx_sort 1` a zákaz příkazu `wait` (skripty/makra).
  - Server běží na tickratu **`40` Hz** (`sv_fps 40`), má opravené slyšení kroků za zdí (`sv_playerBroadcastLimit 15`), zapnutou kompenzaci pingu (`g_antilag 1`) a vypnuté odhazování při zásahu (`g_knockback 0`).
  - Aktivní jsou zPAM opravy hitboxů rukou/torza/krku, opravy double-scroll přebíjení, rychlého lehu (`prone peek`) a MG bugu. Pro čistý obraz a zvuk jsou vypnuté mlha, okolní zvuky, efekty ohně/počasí a shellshock.
- **Komunikace a spectate:** voice chat je vypnutý (textový chat funguje i po smrti), volná spectate kamera, sledování nepřátel i X-Ray streamer systém jsou vypnuté.

---

### Rotace map a v čem jsou `_fix` verze opravené

Na serveru se dokola střídají **3 competitive opravené mapy** z balíku `zpam_maps_v7.iwd` (přehled oprav pochází přímo z oficiálních repozitářů autora):

```text
mp_burgundy_fix  ──▶  mp_carentan_fix  ──▶  mp_toujane_fix
```

#### 1. `mp_burgundy_fix` (FIX v2 — [oficiální repozitář](https://github.com/eyza-cod2/mp_burgundy_fix))
- **Skybox a granáty:** zvýšený skybox, opravené mizení granátů na skyboxu i na Axis spawnu; středový dům (`mid house`) upraven tak, aby odrážel granáty.
- **Lean bugy (chyby textur při vyklánění):** opraveny u spodních dveří a horního okna Allies domu.
- **Zasekávání a překážky:** odstraněny blokující drobnosti na zemi (např. u B chicken), opraveno zasekávání v rohu u kurníku (`henhouse`), u vozíku se senem na B (`B hay cart`), u stromu na Allies spawnu a `wall speed stuck` na zdi Axis domu.
- **Kolize a neviditelné zdi:** opravena neviditelná zeď na Allies spawnu; okno pro skok v Axis domě je pevné (průchozí zůstává v Ready-Up); na Axis sniper domě zachován skok na malou stříšku vedle MG okna.
- **Zvuk a vizuál:** opraven zvuk kročejů v rohu Allies domu ze silnice na dřevo, vizuálně čistší zeď u zahrad na midu a podpora zPAM Aim Traineru. *(Experiment s tichým čupěním na schodech z v1 byl ve v2 zrušen.)*

#### 2. `mp_carentan_fix` (FIX v3 — [oficiální repozitář](https://github.com/eyza-cod2/mp_carentan_fix))
- **Neviditelný hráč a díry ve zdech:** opraven bug neviditelného hráče na plantu B (`B invisible player bug`), opravena díra ve zdi na plantu A i průhledné/nepevné okno uprostřed mapy (`mid`).
- **Lean bugy:** opraveny u dveří budovy u A, u dveří Axis MG domu, u dveří midhousu a u pytlů s pískem (na B, u Axis i na mid street).
- **Granáty a plant:** pásy tanku na A spolehlivě odrážejí granáty; zablokován plant nahoře na vozidle na B (333 FPS jump).
- **Textury, schody a zasekávání:** opraveno zasekávání na chodníku (`pavement stuck`), zvýšený skybox, opravena textura terénu na B, opraveny nepevné/chybějící textury u skoku na střechy i samotné textury střech, doplněna neviditelná kolizní zeď na schodech a podpora zPAM Aim Traineru.

#### 3. `mp_toujane_fix` (FIX v3 — [oficiální repozitář](https://github.com/eyza-cod2/mp_toujane_fix))
- **Skybox a budovy:** zvýšený skybox, opraven bug neviditelného hráče pod střechou A, odstraněna neviditelná neprůstřelná textura na střeše Axis, doplněna chybějící textura v okně Allies a opraveny textury u mid skoku a jump míst.
- **Neviditelný hráč a zasekávání:** opraven bug neviditelného hráče mezi „banánem“ a žebříkem (při zachování originálního vaultingu v rohu „banana spot“), opraveno zasekávání na linku (`link stuck`), `wall-speed stuck` u Allies FOX a `jump peek` u náklaďáku na B.
- **Žebříky a vaulting:** opravena pravá strana žebříku u Allies FOX pro lezení z obou stran, opraveno sklouzávání ze žebříku, opraven vault na zdi u linku a přelez na B balkóně upraven z `OVER` na `ON`. *(Zrušení mid vaultu z v1 bylo ve v3 vráceno zpět do původního stavu.)*
- **Ostatní:** po výbuchu bomby na A/B se zobrazuje model zničeného tanku; přidána podpora zPAM Aim Traineru.

*(Repozitář pro referenci obsahuje také klientské profily v [`main/players/maxXx/config.cfg`](./main/players/maxXx/config.cfg) a [`main/players/maxXx/config_mp.cfg`](./main/players/maxXx/config_mp.cfg).)*

---

## Část 2: Pro administrátory — Konfigurace a nasazení serveru

### Struktura repozitáře (odpovídá adresářům CoD2)

```text
.
├── README.md
└── main/
    ├── cod2server.cfg                 # Hlavní konfigurace dedikovaného serveru
    └── players/
        └── maxXx/
            ├── config.cfg             # Klientský SP config (výchozí profil)
            └── config_mp.cfg          # Klientský MP config (profil maxXx)
```

---

### Použité verze serverového softwaru a oficiální odkazy

Server běží s prázdným `fs_game` (`""`) přímo ze složky `main/`.

| Součást | Použitá verze | Oficiální zdroje a stažení |
| :--- | :--- | :--- |
| **CoD2x (Server)** | `v1.4.6.8` (a novější přes `sv_update 1`) | Repozitář: https://github.com/callofduty2x/CoD2x<br>Release: https://github.com/callofduty2x/CoD2x/releases/tag/v1.4.6.8<br>Linux server: [`CoD2x_1.4.6.8_linux.zip`](https://github.com/callofduty2x/CoD2x/releases/download/v1.4.6.8/CoD2x_1.4.6.8_linux.zip) |
| **zPAM mód + mappack** | `4.12` + `zpam_maps_v7.iwd` | Repozitář: https://github.com/eyza-cod2/zpam3<br>Vydání: https://github.com/eyza-cod2/zpam3/releases<br>Balík: [`zpam412.zip`](https://github.com/eyza-cod2/zpam3/releases/download/4.12/zpam412.zip) |

---

### Přehled nastavení v [`main/cod2server.cfg`](./main/cod2server.cfg)

#### Síť, sloty, bezpečnost a master servery
| Cvar | Hodnota | Popis |
| :--- | :--- | :--- |
| `net_ip` / `net_port` | `"0.0.0.0"` / `"28960"` | Naslouchání na všech rozhraních na výchozím UDP portu `28960` |
| `dedicated` | `2` | Veřejný internetový server |
| `sv_maxclients` | `10` | Maximální počet hráčů |
| `sv_pure` | `1` | Kontrola `.iwd` součtů (nutné pro viditelnost při výchozím filtru `Pure: Yes`) |
| `sv_master1` | `"cod2master.activision.com"` | Hlavní oficiální Activision master server |
| `sv_master2` | `"master.cod2x.me"` | Oficiální CoD2x master server |
| `sv_master3` | `"master.cod.pm"` | Aktivní komunitní CoD master server |
| `sv_maxRate` / `sv_maxPing` | `25000` / `120` | Maximální rychlost `25000 B/s` a horní limit pingu `120 ms` |
| `sv_timeout` / `sv_kickBanTime` | `60` / `300` | Odpojení při výpadku po `60 s`, dočasný ban po `/kick` `5 min` |

#### CoD2x specifické parametry (`callofduty2x/CoD2x`)
| Cvar | Hodnota | Popis |
| :--- | :--- | :--- |
| `g_competitive` | `1` | Vynutí klientům `com_maxfps 125–250`, `rate 25000`, `snaps 40`, `cl_maxpackets 125`, `sc_enable 0`, `fx_sort 1` a blokuje `wait` |
| `sv_fps` | `40` | Tickrate `40` Hz pro synchronizaci se `snaps 40` |
| `sv_cracked` | `1` | Povolí hráče bez originálního CD klíče (HWID bany v `main/ban.txt`) |
| `sv_rateLimiter` | `1` | Ochrana před příchozím UDP floodem / DDoS |
| `sv_playerBroadcastLimit` | `15` | Posílá pozice všech hráčů bez ohledu na PVS portály (oprava neslyšitelných kroků) |
| `sv_wallbang` | `0` | Klasické CoD2 chování bez CoD2x prostřelování zdí |
| `sv_update` | `1` | Automatická aktualizace `libCoD2x.so` při startu Linux serveru |
| `sv_updateZpam` | `1` | Automatická aktualizace zPAM a mappacku na pozadí (v buildech CoD2x 11/2026+) |

#### Herní režim, DM pravidla, zPAM opravy a zbraně
| Cvar | Hodnota | Popis |
| :--- | :--- | :--- |
| `g_gametype` / `pam_mode` | `"dm"` / `"pub"` | Režim `pub` je nutný, aby zPAM respektoval všechna `scr_*` nastavení z configu a po skončení mapy přepnul rotaci přes `exitLevel(false)` (místo `map_restart` v `warmup`) |
| `scr_dm_timelimit` / `scr_dm_end_score` | `30` / `50` | Limit `30` minut nebo `50` bodů pro přepnutí na další mapu |
| `scr_dm_strat_time` / `scr_readyup` / `scr_map_vote` | `0` / `0` / `0` | Bez odpočtu před startem, bez ready-up a pevná rotace podle `sv_mapRotation` |
| `scr_killcam` / `scr_recording` | `0` / `0` | Bez killcamy a bez automatického nahrávání dema hráčům |
| `scr_spectatefree` / `scr_spectateenemy` / `scr_streamersystem` | `0` / `0` / `0` | Vypnutá volná kamera, sledování hráčů po smrti a streamer/X-Ray systém *(pozn.: samotné kliknutí do týmu Spectator nelze přes config zakázat, protože v `_spectating.gsc` pro něj není cvar)* |
| `sv_voice` / `voice_deadChat` / `voice_global` | `0` / `0` / `0` | Úplné vypnutí voice chatu (`g_deadChat 1` zachovává textový chat) |
| `g_knockback` / `g_antilag` | `0` / `1` | Vypnutý knockback („sliding“) a zapnutý antilag |
| `scr_fast_reload_fix` / `scr_prone_peek_fix` / `scr_mg_peek_fix` | `1` | zPAM opravy double-scroll přebíjení, lehu a odhazování MG |
| `scr_hitbox_hand_fix` / `scr_hitbox_torso_fix` / `scr_hitbox_neck_kill` | `1` | zPAM úprava hitboxů rukou, torza a krku |
| `scr_allow_ambient_*` / `scr_allow_shellshock` | `0` | Vypnutí mlhy, ambientních zvuků, ohně, počasí a otřesů při zásahu |
| `scr_*_nades` / `scr_*_smokes` / `scr_allow_shotgun` | `0` | Vypnutí všech granátů, smoků (i dropu po smrti) a brokovnice |

#### FastDL nastavení
- `sv_allowDownload 1`, `sv_wwwDownload 1`, `sv_wwwDlDisconnected 0`
- `sv_wwwBaseURL "http://cod2x.me/zpam"` — je záměrně přes `http://` (bez `s`), protože stabilní vydání **CoD2x `1.4.6.8`** ještě neumí `https://` ve `sv_wwwBaseURL` a při `https://` by klient spadl na pomalé UDP stahování ze serveru. Navíc je oficiální CDN vždy sladěné s `sv_updateZpam 1`.

---

### Nasazení a aktualizace na Proxmox LXC (LinuxGSM)

Server běží pod uživatelem `cod2server` v adresáři `~/serverfiles` s **prázdným `fs_game`** (spouštěcí skript nesmí mít `+set fs_game` nastaveno na modovou složku).

1. **Stažení a instalace `zpam412.zip`:**
   ```bash
   cd /tmp
   wget -O zpam412.zip https://github.com/eyza-cod2/zpam3/releases/download/4.12/zpam412.zip
   unzip -o zpam412.zip -d /tmp/zpam412

   cp /tmp/zpam412/main/zpam412.iwd ~/serverfiles/main/
   cp /tmp/zpam412/main/zpam_maps_v7.iwd ~/serverfiles/main/
   rm -rf /tmp/zpam412 /tmp/zpam412.zip
   ```
   *(Nerozbaluj zip přímo do `~/serverfiles/`, protože obsahuje ukázkový `main/server.cfg`.)*

2. **Nasazení configu a restart:**
   - Zkopíruj [`main/cod2server.cfg`](./main/cod2server.cfg) do `~/serverfiles/main/cod2server.cfg`, nastav vlastní silné `rcon_password` a restartuj server (`./cod2server restart`).

3. **Průběžné aktualizace:**
   - **CoD2x (`sv_update 1`):** automaticky aktualizuje `libCoD2x.so` při startu serveru.
   - **zPAM & mapy (`sv_updateZpam 1`):** v buildech CoD2x podporujících `zpam.json` se nové verze stáhnou na pozadí a aktivují po vyprázdnění serveru; jinak stačí stáhnout novou verzi z [eyza-cod2/zpam3/releases](https://github.com/eyza-cod2/zpam3/releases), vyměnit `.iwd` soubory v `~/serverfiles/main/` a server restartovat.
