# Bloch-gömb szimulátor – Kvantuminformatikai alkalmazások

## Teljes projektdokumentáció

**Készítette:** Varga Marcell Simon és Borvendég Benedek

**Dátum:** 2025. november

**Technológia:** Blazor WebAssembly | C# 8.0+ | Plotly.js 3D vizualizáció

---

## 1. Projektleírás

A **Bloch-gömb szimulátor** egy teljes mértékben böngészőben futó interaktív webalkalmazás, amely lehetővé teszi az egyqubites kvantumállapotok szimulációját, vizualizációját és manipulációját. A program a Bloch-gömb geometriai reprezentációját használja az állapotok megjelenítésére, és lehetőséget biztosít a fő kvantumlogikai kapuk lépésről lépésre vagy egyszerre történő alkalmazására.

### 1.1 Feladat megfelelés

A projekt teljesíti a "Kvantuminformatikai alkalmazások" tárgy házi feladatának összes követelményét:

- ✅ **Webalkalmazás:** Böngészőben futó Blazor WebAssembly
- ✅ **Qubit állapot kezelés:** Komplex amplitúdók szimulációja
- ✅ **Kvantumkapuk:** 10+ logikai kapu (Pauli, Hadamard, forgatások)
- ✅ **Kapu láncolat:** Sorba fűzés és lépésenkénti vagy teljes alkalmazás
- ✅ **Bloch-gömb:** 3D interaktív vizualizáció Plotly.js-sel
- ✅ **Állapotkezelés:** Több állapot mentése és összehasonlítása
- ✅ **Felhasználói élmény:** Intuitív, professzionális UI

---

## 2. Funkciók és Használati Útmutató

### 2.1 Kezdőállapot beállítása

A **"Kezdőállapot"** panel az alkalmazás bal oldali panele.

#### Gyors alapállapot kiválasztás

A **"Gyors beállítás (alapállapotok)"** legördülő menüből 6 előre definiált állapot közül lehet választani:

- $\vert 0 \rangle$ – alapállapot ($\theta = 0°$, $\varphi = 0°$)
- $\vert 1 \rangle$ – gerjesztett állapot ($\theta = 180°$, $\varphi = 0°$)
- $\vert + \rangle$ – szuperponálás az X tengely mentén ($\theta = 90°$, $\varphi = 0°$)
- $\vert - \rangle$ – szuperponálás a −X tengely mentén ($\theta = 90°$, $\varphi = 180°$)
- $\vert +i \rangle$ – szuperponálás az Y tengely mentén ($\theta = 90°$, $\varphi = 90°$)
- $\vert -i \rangle$ – szuperponálás a −Y tengely mentén ($\theta = 90°$, $\varphi = 270°$)

A kiválasztott alapállapot az **"Állapot beállítása"** gombra kattintva aktiválódik.

#### Tetszőleges állapot beállítása

- **$\theta$ (polár szög, radiánban):** 0 és $\pi$ között tetszőleges érték (pl. $\pi/2 \approx 1.5708$)
- **$\varphi$ (azimut szög, radiánban):** 0 és $2\pi$ között tetszőleges érték
- Az állapot a **Bloch-gömbön** az alábbi formulával reprezentálódik:

$$\vert\psi\rangle = \cos\left(\frac{\theta}{2}\right)\vert 0\rangle + e^{i\varphi}\sin\left(\frac{\theta}{2}\right)\vert 1\rangle$$

#### Aktuális állapot megjelenítése

Az **"Aktuális állapot:"** mező alatt a kvantumállapot komplex amplitúdói láthatók:

$$\vert\psi\rangle = \begin{pmatrix} \alpha \\ \beta \end{pmatrix}$$

ahol:
- $\alpha = \cos(\theta/2)$
- $\beta = e^{i\varphi} \sin(\theta/2)$

### 2.2 Logikai kapuk és kapu-sor

A **"Kapuk"** panel az alkalmazás közepén található.

#### Kapu kiválasztása

A **"Kapu:"** legördülő menüből választható:

**Pauli-kapuk:**
- $I$ – Identitás (no operation)
- $X$ – Pauli-X kapu (bit flip)
- $Y$ – Pauli-Y kapu
- $Z$ – Pauli-Z kapu (phase flip)

**Speciális kapuk:**
- $H$ – Hadamard kapu (szuperponálás)
- $S$ – Fáziskapu ($\pi/2$ fáziseltolás)
- $T$ – T-kapu ($\pi/8$ fáziseltolás)

**Parametrizált forgatási kapuk:**
- $R_x(\theta)$ – forgatás az X tengely körül
- $R_y(\theta)$ – forgatás az Y tengely körül
- $R_z(\theta)$ – forgatás a Z tengely körül

#### Forgatási szög beállítása

A **"Forgatási szög ($\theta$, radian):"** mező az $R_x$, $R_y$, $R_z$ kapuknál releváns. Alapértelmezés: 1.5708 ($\pi/2$). Bármilyen radiánérték megadható.

#### Kapu hozzáadása a sorhoz

A **"Hozzáadás"** gombra kattintva az aktuális kapu hozzáadódik a sorhoz.

#### Kapu-sor kezelése

A **"Kapu-sor (pipeline):"** szövegmezőben az összes hozzáadott kapu látható, például: $R_x(1.5708)$, $H$, $Z$, $R_y(3.14159)$.

A sor törlése a **"Sor törlése"** gombbal lehetséges.

#### Kapuk alkalmazása

**Lépésenkénti alkalmazás:**
A **"Következő alkalmazása"** gomb az első kaput alkalmazza a sorból. Az állapot valós időben frissül, a Bloch-gömb azonnal megjeleníti az új pozíciót. Ideális a kapu hatásainak tanulmányozásához.

**Teljes alkalmazás:**
Az **"Összes alkalmazása"** gomb az összes kaput egyszerre futtatja. Az eredmény azonnal látható a Bloch-gömbön.

### 2.3 Pillanatképek (State Snapshots)

A **"Pillanatképek"** panel az alkalmazás jobb oldali panele.

#### Állapot mentése

- **"Azonosító:"** mezzőbe az állapot nevét írjuk (pl. "Hadamard után", "3. iteráció")
- **"Szín:"** szín választó gombra kattintva tetszőleges szín választható
- A **"Mentés"** gomb az aktuális állapotot és annak Bloch-koordinátáit elmenti

#### Mentett állapotok megtekintése

Az összes mentett állapot az alatta lévő listában jelenik meg. Mindegyik állapothoz tartozik egy **kis gömb** az adott szín szerint. Az állapotok így egyszerűen összehasonlíthatók a Bloch-gömbön.

#### Összes állapot törlése

Az **"Összes törlése"** gomb az összes mentett pillanatképet törli.

### 2.4 Bloch-gömb 3D vizualizáció

Az alkalmazás alsó részén megjelenik a **"Bloch-gömb"** panel.

#### Gömb elemei

- **Félátlátszó gömb:** Az egységgömb felülete, amely a lehetséges kvantumállapotok terét reprezentálja
- **Kék pont + vektor:** Az aktuális állapot 3D pozíciója és az origótól induló nyíl
- **Színes pontok:** A mentett állapotok a kiválasztott szín szerint
- **Jelmagyarázat (jobb felső sarok):** Az egyes állapotok azonosítói és szín-hozzárendelése

#### Interakciók

- **Bal klikk + húzás:** A gömb forgatása tetszőleges irányba
- **Görgetés:** Nagyítás és kicsinyítés
- **Jobb klikk + mozgás:** 3D térben való mozgatás (pan)
- **Egér lebegés az állapoton:** Az adott állapot Bloch-koordinátái (x, y, z értékei) megjelennek

#### Bloch-koordináták

Az $(x, y, z)$ koordináták a Bloch-gömb felületén az alábbiak szerint számítódnak:

$$x = 2 \text{Re}(\alpha^* \beta)$$

$$y = 2 \text{Im}(\alpha^* \beta)$$

$$z = |\alpha|^2 - |\beta|^2$$

ahol $\alpha$ és $\beta$ a qubit amplitúdói.

---

## 3. Technikai Implementáció

### 3.1 Architektura

A projekt **Blazor WebAssembly** keretrendszerre épül, amely lehetővé teszi a C# kód böngészőben való futtatását WebAssembly (WASM) formában.

**Komponensek:**

1. **Frontend (Razor Components):** Interaktív UI elemek (beviteli mezők, gombok, legördülő menük), valós idejű állapotfrissítés, Bloch-gömb vizualizáció integrálása

2. **Backend szolgáltatás (QuantumService):** Kapu mátrixok definiálása, állapotmanipuláció, Bloch-vektor számítás, normalizáció és mátrix szorzás

3. **Vizualizáció (Plotly.js):** 3D gömb mesh generálása, pontok és vektorok renderelése, interaktív kontrollerek

### 3.2 Kvantumállapot kezelés

Minden qubit állapot egy **2D komplex vektorként** reprezentálódik:

$$\vert\psi\rangle = \begin{pmatrix} \alpha \\ \beta \end{pmatrix}, \quad |\alpha|^2 + |\beta|^2 = 1$$

A normalizáció biztosítja, hogy az állapot mindig egységvektormarad.

### 3.3 Kapu mátrixok

Minden logikai kapu egy **2×2 unitér mátrix** formájában reprezentálódik:

**Pauli-kapuk:**

$$I = \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix}, \quad X = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}$$

$$Y = \begin{pmatrix} 0 & -i \\ i & 0 \end{pmatrix}, \quad Z = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}$$

**Hadamard:**

$$H = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix}$$

**Fáziskapuk:**

$$S = \begin{pmatrix} 1 & 0 \\ 0 & i \end{pmatrix}, \quad T = \begin{pmatrix} 1 & 0 \\ 0 & e^{i\pi/4} \end{pmatrix}$$

**Forgatási kapuk:**

$$R_x(\theta) = \begin{pmatrix} \cos(\theta/2) & -i\sin(\theta/2) \\ -i\sin(\theta/2) & \cos(\theta/2) \end{pmatrix}$$

$$R_y(\theta) = \begin{pmatrix} \cos(\theta/2) & -\sin(\theta/2) \\ \sin(\theta/2) & \cos(\theta/2) \end{pmatrix}$$

$$R_z(\theta) = \begin{pmatrix} e^{-i\theta/2} & 0 \\ 0 & e^{i\theta/2} \end{pmatrix}$$

### 3.4 Kapu alkalmazás

Egy kapu alkalmazása az állapotra:

$$\vert\psi'\rangle = U \vert\psi\rangle$$

Ez mátrix-vektor szorzásként implementálódik a `QuantumService`-ben.

---

## 4. Telepítés és Futtatás

### 4.1 Rendszerkövetelmények

- Modern webböngésző (Chrome, Firefox, Edge, Safari)
- JavaScript engedélyezve
- WebAssembly támogatás

### 4.2 Futtatás

Az alkalmazás teljes mértékben statikus – nincs szerver szükséges!

**Opció 1: Helyi fájlokból**
1. Töltsd le a projektdokumentáció **wwwroot** mappáját
2. Nyisd meg az `index.html` fájlt webböngészőben
3. Az alkalmazás azonnal működik

**Opció 2: GitHub Pages (már publikálva)**
- Az alkalmazás érhető el a GitHub Pages-en az Ön repositoryjában
- Közvetlen link az `index.html`-hez

### 4.3 Függőségek

- **Plotly.js:** 3D vizualizáció (CDN-ről betöltve)
- **Bootstrap CSS:** Alapvető stílusok (közbeeső függőség)

---

## 5. Felhasználási Esetek és Példák

### Eset 1: $\vert 0 \rangle \to \vert 1 \rangle$ transzformáció az X kapuval

1. Kezdőállapot: $\theta = 0$, $\varphi = 0$ ($\vert 0 \rangle$)
2. Kapu: $X$
3. "Hozzáadás" → "Következő alkalmazása"
4. Eredmény: Az állapot a Bloch-gömb tetejéről az aljára mozdul

### Eset 2: Szuperponálás Hadamard kapuval

1. Kezdőállapot: $\theta = 0$, $\varphi = 0$ ($\vert 0 \rangle$)
2. Kapu: $H$
3. "Hozzáadás" → "Következő alkalmazása"
4. Eredmény: Az állapot az egyenlítőre kerül ($\vert + \rangle = (\vert 0 \rangle + \vert 1 \rangle)/\sqrt{2}$)

### Eset 3: Forgatás és összehasonlítás

1. Állapot 1 beállítása: $\theta = \pi/2$, $\varphi = 0$
2. "Pillanatkép mentése" (szín: kék) – "Állapot 1"
3. Kapu: $R_z(\pi/4)$ alkalmazása
4. "Pillanatkép mentése" (szín: piros) – "$R_z(\pi/4)$ után"
5. Mindkét állapot látható a Bloch-gömbön, lehet azokat összehasonlítani

---

## 6. Fejlesztési Megjegyzések

### 6.1 Kódminőség

- ✅ Típusos C# kód (no null reference exceptions)
- ✅ Dokumentált függvények
- ✅ Matematikai pontosság (complex számok)
- ✅ Moduláris architektúra

### 6.2 Reszponzivitás

- Az alkalmazás **mobilra optimalizált**, de a Bloch-gömb teljes mérete asztali nézetben javasolt
- Tableten: a három panel 2 sorban jelenik meg
- Mobilon: a panelok egymás alatt vannak

### 6.3 Teljesítmény

- Böngészőben futó WASM: szupergyors állapotfellépések
- Nincsenek hálózati kérések – 100% offline működés
- Plotly.js: optimalizált 3D renderelés

---

## 7. Etikai és Szerzői Megjegyzések

### 7.1 Szerzőség

- **Készítette:** Varga Marcell Simon és Borvendég Benedek
- **Technológia:** Blazor WebAssembly, C# 8.0+, Plotly.js

### 7.2 Mesterséges intelligencia alkalmazása

A projektfejlesztésben felhasználtam AI asszisztenciát:
- Kódstruktúra és best practices
- Dokumentáció írása
- Tesztelés és hibakeresés
- UI/UX javaslatok

**Minden kód szakmailag ellenőrzött, az algoritmusok helyesek, és a végeredmény teljes mértékben működőképes.**

### 7.3 Licence

Az alkalmazás szabadon használható oktatási célokra. A Plotly.js MIT licenc alatt áll.

---

## 8. Hibaelhárítás

| Probléma | Megoldás |
|----------|----------|
| Az alkalmazás nem töltődik be | Ellenőrizd, hogy a böngésző támogatja a WebAssembly-t (Chrome, Firefox, Edge 79+) |
| A Bloch-gömb nem jelenik meg | Töltsd be a böngészt (F5), biztosítsd, hogy a Plotly.js CDN elérhető |
| Az állapot nem frissül | Kattints az "Állapot beállítása" gombra, ellenőrizd az értékeket ($\theta \in [0,\pi]$, $\varphi \in [0,2\pi]$) |
| A pillanatképek nem jelennek meg | Győződj meg, hogy legalább egy állapotot mentettél |

---

## 9. Tesztelési Protokoll

Az alkalmazás az alábbi tesztek alapján validálódott:

**Funkcionális tesztek:**
- Állapot beállítása (mind a 6 alapállapot)
- Kapu hozzáadása és alkalmazása (mind a 10 kapu)
- Forgatási szögek ($0, \pi/2, \pi, 2\pi$)
- Pillanatképek mentése és törlése

**Vizualizációs tesztek:**
- Bloch-gömb renderelése
- Pont mozgása az állapot változásakor
- Vektor megjelenítése
- Interaktivitás (forgatás, zoom, pan)

**Reszponzív tesztek:**
- Desktop (1920x1080)
- Tablet (768px)
- Mobil (360px)

**Teljesítménytesztek:**
- 50+ kapu láncolat (nem lassú)
- 20+ pillanatkép (memória oka)

---

## 10. Jövőbeli Fejlesztési Lehetőségek

- [ ] Két qubites kapuk (CNOT, CZ)
- [ ] Mérési szimuláció (Born-szabály)
- [ ] Nyomtracefüggvények
- [ ] Kapu reverz lehetőség
- [ ] Közvetlenül szerkeszthető Bloch-koordináták
- [ ] Animált átmenetések az állapotok között
- [ ] Kvantummechanikai megoldók

---

## 11. Összefoglalás

A **Bloch-gömb szimulátor** egy professzionális, teljes körűen működő webalkalmazás, amely lehetővé teszi a kvantumállapotok intuitív tanulmányozását. Az alkalmazás:

- ✅ Teljesíti az összes feladat követelményt
- ✅ Matematikailag pontos
- ✅ Felhasználóbarát és intuitív
- ✅ Képernyőn azonnal futtatható
- ✅ Nyílt forráskódú és kiterjeszthető

**Az alkalmazás kész a beadásra és az oktatási felhasználatra.**

---

## Függelék: Rövid Matematikai Összefoglalás

### A.1 Qubit alapok

A qubit (quantum bit) egy kvantumrendszer alapegysége, amely két bázisállapottal rendelkezik: $\vert 0 \rangle$ és $\vert 1 \rangle$. Egy általános állapot ezek szuperponíciója:

$$\vert\psi\rangle = \alpha \vert 0\rangle + \beta \vert 1\rangle$$

ahol $\alpha$ és $\beta$ komplex számok, és $|\alpha|^2 + |\beta|^2 = 1$ (normalizáció).

### A.2 Bloch-gömb reprezentáció

A Bloch-gömb az egyqubites kvantumállapotok geometriai reprezentációja. Egy tetszőleges qubit állapot egyértelműen megfeleltetethető a Bloch-gömb felületének egy pontjának az alábbi koordinátákon keresztül:

$$(x, y, z) = \left(2\text{Re}(\alpha^* \beta), 2\text{Im}(\alpha^* \beta), |\alpha|^2 - |\beta|^2\right)$$

A gömb felülete az összes lehetséges (normalizált) egyqubites állapotot reprezentálja.

### A.3 Unitér transzformációk

Kvantumműveletek unitér mátrixok által reprezentálódnak. A kapu alkalmazása:

$$\vert\psi'\rangle = U \vert\psi\rangle$$

ahol $U$ egy unitér mátrix ($U^\dagger U = I$).

### A.4 Bloch-vektor és forgatások

A Bloch-gömb pontjainak forgatása az origó körül a $R_i(\theta)$ forgatási mátrixok segítségével történik. Az $i$ tengely körüli $\theta$ szögű forgatás az alábbi hatást gyakorolja a Bloch-vektorra:

$$\vec{r}' = \begin{pmatrix} 1 & 0 & 0 \\ 0 & \cos\theta & -\sin\theta \\ 0 & \sin\theta & \cos\theta \end{pmatrix} \vec{r} \quad (i = x \text{eset})$$

Hasonló képletek alkalmazandók az $y$ és $z$ tengelyek esetén is.

---

**Dokumentáció vége**

*A dokumentáció 2025. november 22-én készült.*

*Bloch-gömb szimulátor © 2025 Varga Marcell Simon és Borvendég Benedek*
