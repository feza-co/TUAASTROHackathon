<!--
Hey, thanks for using the awesome-readme-template template.  
If you have any enhancements, then fork this project and create a pull request 
or just open an issue with the label "enhancement".

Don't forget to give this project a star for additional support ;)
Maybe you can mention me or this repo in the acknowledgements too
-->
<div align="center">

  <img src="assets/logo.png" alt="logo" width="200" height="auto" />
  <h1>LunaPath</h1>
  
  <p>
    Ay güney kutbu yükseklik verisinden türetilen analiz ızgaraları üzerinde eğim, enerji, gölge ve termal riski birlikte değerlendirerek rover rotası üreten çok kriterli navigasyon prototipi. 
  </p>
  
  
<!-- Badges -->
<p>
  <a href="">
    <img src="https://img.shields.io/github/contributors/feza-co/TUAASTROHackathon" alt="contributors" />
  </a>
  <a href="">
    <img src="https://img.shields.io/github/last-commit/feza-co/TUAASTROHackathon" alt="last update" />
  </a>
  <a href="">
    <img src="https://img.shields.io/github/forks/feza-co/TUAASTROHackathon" alt="forks" />
  </a>
  <a href="">
    <img src="https://img.shields.io/github/stars/feza-co/TUAASTROHackathon" alt="stars" />
  </a>
  <a href="">
    <img src="https://img.shields.io/github/issues/feza-co/TUAASTROHackathon" alt="open issues" />
  </a>
  <a href="">
    <img src="https://img.shields.io/github/license/feza-co/TUAASTROHackathon.svg" alt="license" />
  </a>
</p>
   
<h4>
    <a href="">View Demo</a>
  <span> · </span>
    <a href="">Documentation</a>
  <span> · </span>
    <a href="">Report Bug</a>
  <span> · </span>
    <a href="">Request Feature</a>
  </h4>
</div>

<br />

<!-- Table of Contents -->
# :notebook_with_decorative_cover: Table of Contents

- [About the Project](#star2-about-the-project)
  * [Screenshots](#camera-screenshots)
  * [Tech Stack](#space_invader-tech-stack)
  * [Features](#dart-features)
  * [Color Reference](#art-color-reference)
  * [Environment Variables](#key-environment-variables)
- [Getting Started](#toolbox-getting-started)
  * [Prerequisites](#bangbang-prerequisites)
  * [Installation](#gear-installation)
  * [Running Tests](#test_tube-running-tests)
  * [Run Locally](#running-run-locally)
  * [Deployment](#triangular_flag_on_post-deployment)
- [Usage](#eyes-usage)
- [Roadmap](#compass-roadmap)
- [Contributing](#wave-contributing)
  * [Code of Conduct](#scroll-code-of-conduct)
- [FAQ](#grey_question-faq)
- [License](#warning-license)
- [Contact](#handshake-contact)
- [Acknowledgements](#gem-acknowledgements)

  

<!-- About the Project -->
## :star2: About the Project

LunaPath, TUA ASTRO Hackathon kapsamında geliştirilen bir Ay yüzeyi rota planlama prototipidir. NASA LRO/LOLA kaynaklı bir sayısal yükseklik modelinden (DEM) yedi analiz katmanı üretir, bu katmanları ağırlıklı bir maliyet alanına dönüştürür ve A\* algoritmasıyla rover için geçilebilir bir koridor hesaplar. Rota bulunduktan sonra üzerinde adım adım enerji, batarya ve termal risk simülasyonu çalıştırılır.

Sistem üç bileşenden oluşur:

| Klasör | Rol |
|--------|-----|
| `lunapath/` | P1 veri işleme hattı: DEM'den `.npy` ızgaraları ve `metadata.json` üretir |
| `backend/` | FastAPI servisi: maliyet motoru, A\* planlayıcı, simülasyon ve REST uçları |
| `frontend/` | React + TypeScript arayüzü: 3D karşılama sahnesi ve 2D görev kontrol ekranı |
| `docs/` | Teknik referans belgesi, formüller, ön işleme raporu ve tasarım notları |

Varsayılan çalışma alanı Ay güney kutbunda 500 × 500 hücrelik bir pencere, 80 m/piksel çözünürlükte (yaklaşık 40 × 40 km), Ay güney kutup stereografik projeksiyonundadır.

Analiz katmanları fiziksel olarak birbirine bağlıdır: yükseklikten eğim ve bakı, bunlardan sentetik yüzey sıcaklığı, yükseklikten gölge oranı, hepsinden geçilebilirlik maskesi ve ağırlıklı maliyet ızgarası türetilir. Geçilebilirlik ve maliyet mantığı tek bir kaynak modülde tutulur (`backend/app/traversability.py`, `backend/app/cost_engine.py`); veri hattı da API de aynı modülleri kullanır.

<!-- Screenshots -->
### :camera: Screenshots

<div align="center"> 
  <img src="https://placehold.co/600x400?text=Your+Screenshot+here" alt="screenshot" />
</div>

[TODO: Görev kontrol ekranının ve 3D karşılama sahnesinin ekran görüntüleri depoya eklenmemiş. `lunapath/data/processed/` altındaki `environment_dashboard.png`, `lunar_surface_dem.png` ve `thermal_risk_plot.png` dosyaları `.gitignore` ile hariç tutulduğu için buraya bağlanamaz; ekran görüntülerini sürüm kontrolüne dahil edilen bir klasöre (örn. `assets/`) koyup bağlantıyı güncelleyin.]

[TODO: `assets/logo.png` dosyası depoda yok. Logo eklenene kadar üstteki görsel bozuk görünecektir.]

<!-- TechStack -->
### :space_invader: Tech Stack

<details>
  <summary>Client</summary>
  <ul>
    <li><a href="https://react.dev/">React 18</a></li>
    <li><a href="https://www.typescriptlang.org/">TypeScript 5</a></li>
    <li><a href="https://vitejs.dev/">Vite 5</a></li>
    <li><a href="https://threejs.org/">three.js 0.183 (3D karşılama sahnesi)</a></li>
    <li><a href="https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API">Canvas 2D API (ızgara ve rota render'ı)</a></li>
  </ul>
</details>

<details>
  <summary>Server</summary>
  <ul>
    <li><a href="https://www.python.org/">Python 3.11+</a></li>
    <li><a href="https://fastapi.tiangolo.com/">FastAPI 0.115</a></li>
    <li><a href="https://www.uvicorn.org/">Uvicorn 0.34</a></li>
    <li><a href="https://docs.pydantic.dev/">Pydantic v2 (istek doğrulama)</a></li>
    <li><a href="https://numpy.org/">NumPy 2.2</a></li>
    <li><a href="https://scipy.org/">SciPy 1.15</a></li>
    <li><a href="https://rasterio.readthedocs.io/">rasterio 1.4 (GDAL)</a></li>
    <li><a href="https://pyproj4.github.io/pyproj/">pyproj 3.7 (koordinat dönüşümü)</a></li>
    <li><a href="https://matplotlib.org/">Matplotlib (veri hattı görselleştirmesi)</a></li>
  </ul>
</details>

<details>
<summary>Database</summary>
  <ul>
    <li>Veritabanı kullanılmaz. Izgaralar diskte NumPy <code>.npy</code> dosyaları, ızgara tanımı ise <code>metadata.json</code> olarak tutulur.</li>
    <li>Backend, DEM'den türetilen ızgaraları <code>backend/data/cache/</code> altında ağırlık karmasına göre önbelleğe alır.</li>
  </ul>
</details>

<details>
<summary>DevOps</summary>
  <ul>
    <li>[TODO: Depoda CI/CD tanımı, Dockerfile veya dağıtım yapılandırması bulunmuyor.]</li>
  </ul>
</details>

<!-- Features -->
### :dart: Features

- **Yedi katmanlı veri hattı** — Tek bir DEM dosyasından yükseklik, eğim, bakı, gölge oranı, termal, geçilebilirlik ve maliyet ızgaraları üretir; en yüksek yükseklik farkı × eğim varyansına sahip 500 × 500 pencereyi otomatik seçer.
- **Çok kriterli maliyet motoru** — Eğim (sigmoid), enerji (fiziksel sürtünme ve eğim modeli), gölge (kümülatif üstel) ve termal (çift sigmoid) cezalarını AHP ağırlıklarıyla birleştirir. Planlama sırasında kullanılan model, `metadata.json` içinde de kayıtlı olan `weighted_cell_cost_without_barrier`'dır: hücre bazlı ağırlıklı maliyet, log-bariyer terimi olmadan. Bariyer formülasyonu (`cost_engine.total_edge_cost`, `log_barrier_penalty`) tam kenar maliyeti modeli için mevcuttur ancak hızlı A\* yolunda çağrılmaz.
- **Optimize A\* planlayıcı** — 8 yönlü hareket, oktil sezgisel, yamuk kenar interpolasyonu, köşe kesme koruması ve erken çıkış; NumPy dizileri ve `heapq` ile çalışır.
- **Rota simülasyonu** — Adım adım batarya yüzdesi, enerji tüketimi, geçen süre, gölge maruziyeti, yeniden şarj olayları ve `LOW`/`MEDIUM`/`HIGH`/`CRITICAL` risk sınıfı üretir.
- **Çoklu rover kataloğu** — LPR-1 (varsayılan), LUVMI-M, NASA VIPER ve CNSA Yutu-2; her biri kendi kütle, hız, batarya, eğim limiti, gölge dayanımı ve termal zarf değerleriyle. Rover değişimi geçilebilirlik ve maliyet ızgaralarını yeniden hesaplar.
- **Görev profilleri** — Dengeli Keşif, Enerji Tasarrufu, Hızlı Keşif ve Gölge Geçiş profilleri; `/api/compare` ile aynı başlangıç-hedef çifti için karşılaştırmalı sonuç ve öneri döner.
- **REST API** — 12 uç nokta; `http://127.0.0.1:8000/docs` üzerinden etkileşimli olarak denenebilir.
- **Görev kontrol arayüzü** — Yedi görüntüleme modu (yüzey, termal, maliyet, gölge, geçilebilirlik, eğim, bakı), tıklayarak başlangıç/hedef seçimi, canlı ağırlık kaydırıcıları, hücre telemetrisi, batarya halkası, risk dağılımı ve rota oynatma animasyonu.
- **3D karşılama sahnesi** — three.js ile LROC WAC global dokusu üzerine kurulu, göreve geçişte kamera animasyonu yapan Ay küresi.
- **Matplotlib panosu** — İşlenmiş ızgaralar için doğrulama grafikleri ve çevre panosu üretir.

<!-- Color Reference -->
### :art: Color Reference

| Color             | Hex                                                                |
| ----------------- | ------------------------------------------------------------------ |
| Primary Color | ![#13131b](https://via.placeholder.com/10/13131b?text=+) #13131b |
| Secondary Color | ![#1f1f28](https://via.placeholder.com/10/1f1f28?text=+) #1f1f28 |
| Accent Color | ![#c2c1ff](https://via.placeholder.com/10/c2c1ff?text=+) #c2c1ff |
| Text Color | ![#e4e1ed](https://via.placeholder.com/10/e4e1ed?text=+) #e4e1ed |

Durum renkleri (`frontend/src/App.css` ve rota risk göstergeleri):

| Color             | Hex                                                                |
| ----------------- | ------------------------------------------------------------------ |
| Safe / LOW | ![#00e676](https://via.placeholder.com/10/00e676?text=+) #00e676 |
| Caution / MEDIUM | ![#ffea00](https://via.placeholder.com/10/ffea00?text=+) #ffea00 |
| High | ![#ff6d00](https://via.placeholder.com/10/ff6d00?text=+) #ff6d00 |
| Critical | ![#ff1744](https://via.placeholder.com/10/ff1744?text=+) #ff1744 |

<!-- Env Variables -->
### :key: Environment Variables

To run this project, you will need to add the following environment variables to your .env file

Projenin çalışması için **zorunlu ortam değişkeni yoktur.** `.env` dosyası gerekmez; kod tabanında dışarıdan okunan bir yapılandırma değişkeni bulunmamaktadır. Aşağıdaki iki değişken kod içinde kullanılır ancak elle ayarlanması gerekmez:

| Değişken | Nerede | Açıklama |
|----------|--------|----------|
| `PROJ_IGNORE_CELESTIAL_BODY` | `backend/app/serializer.py` | `os.environ.setdefault` ile `YES` olarak atanır. pyproj'un Ay CRS'i için Dünya dışı gövde uyarısını bastırır. |
| `LUNAPATH_SKIP_STARTUP` | `backend/test_plan_endpoint.py` | Yalnızca test dosyası tarafından atanır; uygulama kodu bu değeri okumaz. |

[TODO: `.gitignore` bir `.env.example` dosyasına atıfta bulunuyor ancak depoda böyle bir dosya yok. İleride yapılandırılabilir bir ayar eklenirse örnek dosya da oluşturulmalı.]

<!-- Getting Started -->
##  :toolbox: Getting Started

<!-- Prerequisites -->
### :bangbang: Prerequisites

- **Python 3.11+** — Kod tabanı `X | None` biçimli tip söz dizimi ve NumPy 2.x kullanır.
- **Node.js 18+** ve npm — Vite 5 gereksinimi.
- **GDAL** — `rasterio` ikili bağımlılığı. Windows'ta hazır wheel ile, Linux/macOS'ta sistem GDAL paketiyle kurulur; kurulum işletim sistemine göre değişir.
- **DEM dosyası** — Veri hattını çalıştırmak için `LDEM_80S_80MPP_ADJ.tiff` (NASA LRO/LOLA, Ay güney kutbu, 80 m/piksel). Dosya boyutu nedeniyle depoya dahil edilmemiştir.
- **Git** — Depoyu klonlamak için.

<!-- Installation -->
### :gear: Installation

Depoyu klonlayın:

```bash
git clone https://github.com/feza-co/TUAASTROHackathon.git
cd TUAASTROHackathon
```

Backend ve veri hattı için tek bir sanal ortam kullanın. `lunapath/src/process_lunar_data.py`, `backend/app` modüllerini içe aktardığı için her iki gereksinim dosyası aynı ortama kurulur:

```bash
python -m venv .venv
# Windows:
.venv\Scripts\activate
# Linux/macOS:
source .venv/bin/activate

pip install -r backend/requirements.txt
pip install -r lunapath/requirements.txt
```

Frontend bağımlılıkları:

```bash
cd frontend
npm install
```
   
<!-- Running Tests -->
### :test_tube: Running Tests

Backend testleri `pytest` ile çalışır. `pytest` gereksinim dosyalarında listelenmediği için ayrıca kurulmalıdır:

```bash
pip install pytest
cd backend
pytest
```

Tek bir test dosyası için:

```bash
cd backend
pytest test_plan_endpoint.py -v
```

Test kapsamı: A\* planlayıcı (`test_astar_standalone.py`), maliyet motoru (`test_cost_engine.py`), API uçları (`test_plan_endpoint.py`), yanıt serileştirme (`test_serializer.py`), simülasyon (`test_simulation.py`), geçilebilirlik (`test_traversability.py`) ve ağırlık entegrasyonu (`test_weighted_integration.py`). Veri hattı tarafında `lunapath/src/test_grid_logic.py` ve `lunapath/src/test_visualize.py` bulunur.

Frontend tip denetimi:

```bash
cd frontend
npm run typecheck
```

[TODO: `frontend/package.json` içinde bir `lint` betiği tanımlı ancak `eslint` ve eklentileri `devDependencies` altında yer almıyor; `npm run lint` mevcut durumda çalışmaz. Ya eslint bağımlılıkları eklenmeli ya da betik kaldırılmalıdır.]

<!-- Run Locally -->
### :running: Run Locally

**1. Backend'i başlatın** (varsayılan port `8000`):

```bash
cd backend
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

Etkileşimli API dokümantasyonu: `http://127.0.0.1:8000/docs`

Backend açılışta `lunapath/data/processed/` altındaki `.npy` ızgaralarını yüklemeyi dener. Dosyalar yoksa uyarı verir ve planlama uçları veri yüklenene kadar `503` döner.

**2. Veri hattını çalıştırın** (ızgaralar henüz üretilmemişse):

DEM dosyasını `lunapath/data/raw/` (ya da depo kökündeki `data/raw/`) klasörüne `LDEM_80S_80MPP_ADJ.tiff` adıyla koyun, sonra:

```bash
cd lunapath/src
python process_lunar_data.py
```

Ağırlıkları geçersiz kılmak için:

```bash
python process_lunar_data.py --weights-json '{"w_slope":0.7,"w_energy":0.1,"w_shadow":0.1,"w_thermal":0.1}'
```

Çıktılar `lunapath/data/processed/` altına yazılır. Ardından backend'e yükletin:

```bash
curl -X POST http://127.0.0.1:8000/api/load-preprocessed \
  -H "Content-Type: application/json" -d "{}"
```

**3. Frontend'i başlatın** (port `3000`, `/api` istekleri `localhost:8000`'e proxy'lenir):

```bash
cd frontend
npm run dev
```

Arayüz `http://localhost:3000` adresinde açılır ve açılışta sağlık kontrolü yapıp gerekirse ızgaraları kendisi yükler.

**4. Görsel özet üretin** (isteğe bağlı, işlenmiş `.npy` dosyaları hazırsa):

```bash
cd lunapath/src
python visualize_processed_data.py
```

**Üretim derlemesi:**

```bash
cd frontend
npm run build
```

<!-- Deployment -->
### :triangular_flag_on_post: Deployment

[TODO: Depoda dağıtım yapılandırması bulunmuyor — Dockerfile, `docker-compose.yml`, CI/CD iş akışı veya platform yapılandırması yok. Şu anda proje yalnızca yerel geliştirme ortamında çalıştırılmak üzere tasarlanmıştır.]

Dağıtım eklenene kadar gereken asgari adımlar:

```bash
# Frontend statik dosyalarını üret
cd frontend
npm run build   # çıktı: frontend/dist/

# Backend'i üretim sunucusuyla çalıştır
cd backend
uvicorn app.main:app --host 0.0.0.0 --port 8000
```

Not: `backend/app/main.py` içindeki CORS ara katmanı tüm kökenlere izin verir (`allow_origins=["*"]`). Genel erişime açık bir dağıtımdan önce bu ayar daraltılmalıdır.

<!-- Usage -->
## :eyes: Usage

**Arayüz üzerinden:** Karşılama ekranındaki keşif düğmesiyle görev kontrol ekranına geçin. Sağ üstteki mod düğmeleriyle katmanı seçin, haritada başlangıç ve hedef noktasını tıklayın, sol paneldeki rover ve öncelik kaydırıcılarını ayarlayın, ardından **Generate Route** ile rotayı üretin. Sağ panel batarya, risk dağılımı ve ara nokta özetini gösterir.

**API üzerinden:**

Sağlık kontrolü ve ızgara durumu:

```bash
curl http://127.0.0.1:8000/api/health
```

Rover kataloğu:

```bash
curl http://127.0.0.1:8000/api/rovers
```

Piksel koordinatıyla rota planlama:

```bash
curl -X POST http://127.0.0.1:8000/api/plan \
  -H "Content-Type: application/json" \
  -d '{
    "start": {"row": 100, "col": 100},
    "goal":  {"row": 400, "col": 400},
    "rover_id": "nasa_viper",
    "weights": {"w_slope": 0.409, "w_energy": 0.259, "w_shadow": 0.142, "w_thermal": 0.19},
    "include_simulation": true
  }'
```

Coğrafi koordinatla planlama (`row`/`col` yerine `lon`/`lat`). Değerler yüklü pencerenin içine düşmelidir; varsayılan 500 × 500 pencere yaklaşık `67.8°–74.7°D` boylam ve `-82.3°–-84.0°` enlem aralığını kapsar:

```bash
curl -X POST http://127.0.0.1:8000/api/plan \
  -H "Content-Type: application/json" \
  -d '{"start": {"lon": 73.0725, "lat": -83.6637}, "goal": {"lon": 68.9625, "lat": -82.6608}}'
```

Pencere sınırlarını bilmiyorsanız bir pikselin gerçek koordinatını `/api/cell-telemetry` ile öğrenip bu uca geçirebilirsiniz. Enlemi `-80°`'in kuzeyine düşen değerler `422` döner.

Tüm görev profillerini karşılaştırma:

```bash
curl -X POST http://127.0.0.1:8000/api/compare \
  -H "Content-Type: application/json" \
  -d '{"start": [100, 100], "goal": [400, 400], "rover_id": "lpr_1"}'
```

Katman verisi çekme (alt örnekleme ile):

```bash
curl "http://127.0.0.1:8000/api/layers/thermal?downsample=4"
```

Hücre telemetrisi:

```bash
curl "http://127.0.0.1:8000/api/cell-telemetry?row=250&col=250"
```

**Uç nokta özeti:**

| Yöntem | Yol | Açıklama |
|--------|-----|----------|
| `GET` | `/api/health` | Servis durumu, yüklü ızgara ve boyut bilgisi |
| `GET` | `/api/rovers` | Rover kataloğu ve varsayılan ağırlıklar |
| `POST` | `/api/load-preprocessed` | P1 hattının ürettiği `.npy` ızgaralarını yükler |
| `POST` | `/api/load-dem` | `backend/data/dem/` altındaki bir DEM'i işleyip yükler |
| `GET` | `/api/cell-telemetry` | Tek hücre için koordinat, yükseklik ve sıcaklık |
| `POST` | `/api/plan` | Tek rota planlar ve simülasyon çalıştırır |
| `POST` | `/api/plan-multi` | Seçilen profiller için çoklu rota planlar |
| `POST` | `/api/compare` | Tüm profilleri karşılaştırır ve öneri döner |
| `GET` | `/api/layers/{layer_name}` | Katman verisi (`elevation`, `slope`, `aspect`, `thermal`, `shadow_ratio`, `cost`, `traversable`) |
| `GET` | `/api/profiles` | Görev profilleri, ağırlıkları ve kısıtları |
| `GET` | `/api/scenarios` | Tanımlı senaryo listesi (depoda tanımlı senaryo yoktur; `backend/data/scenarios/` boş oluşturulur ve uç `[]` döner) |
| `POST` | `/api/scenarios/{scenario_id}/load` | Senaryoyu ve varsa DEM'ini yükler (senaryo dosyası olmadığından şu anda `404` döner) |

**Ağırlıklar:** `w_slope`, `w_energy`, `w_shadow`, `w_thermal` değerleri `[0.0, 2.0]` aralığında olmalıdır; aralık dışı değerler `422` döner. Ağırlık verilmezse seçili rover'ın varsayılan AHP profili kullanılır.

<!-- Roadmap -->
## :compass: Roadmap

* [ ] Sentetik termal ızgarayı gerçek ölçüm verisiyle değiştirmek (LRO Diviner yüzey sıcaklığı). Şu anda sıcaklık, `backend/app/thermal_grid.py` içinde yükseklik, eğim ve bakıdan türetilen bir modeldir.
* [ ] Yükseklik tabanlı gölge vekilini gerçek ufuk/aydınlanma hesabıyla (ray-casting veya efemeris tabanlı) değiştirmek.
* [ ] `backend/app/pathfinder.py` içindeki sabit `_CELL_M = 80.0` değerini `metadata.resolution_m` üzerinden okumak; farklı çözünürlükte ızgaralarda mesafe hesabı şu anda hatalı olur.
* [ ] `astar()` fonksiyonuna geçirilen `constraints` parametresini etkin hale getirmek; hızlı modda şu anda yalnızca API uyumluluğu için kabul edilip yok sayılıyor.
* [ ] `cost_engine.total_edge_cost` ve `log_barrier_penalty` fonksiyonlarını planlama yoluna dahil etmek. Bu iki fonksiyon ile eğim/SOC/termal kısıt bariyerleri yazılmış durumda ancak `pathfinder.py` yalnızca `compute_cost_grid` kullandığı için hiç çağrılmıyor — `constraints` parametresinin yok sayılmasıyla aynı kök nedene sahip.
* [ ] Dağıtım yapılandırması eklemek (Dockerfile, CI iş akışı) ve üretim için CORS politikasını daraltmak.
* [ ] `eslint` bağımlılıklarını ekleyip `npm run lint` betiğini çalışır hale getirmek.
* [ ] `contributing.md` ve davranış kuralları dosyalarını oluşturmak.


<!-- Contributing -->
## :wave: Contributing

Contributions are always welcome!

See `contributing.md` for ways to get started.

[TODO: Depoda `contributing.md` dosyası bulunmuyor. Katkı yönergeleri hazırlanana kadar depo sahipleriyle bir konu (issue) üzerinden iletişime geçin.]

Katkı akışı için mevcut dal adlandırması ve commit biçimi:

```bash
git checkout -b feature/kisa-aciklama
git commit -m "feat(backend): kisa aciklama"
```

<!-- Code of Conduct -->
### :scroll: Code of Conduct

Please read the Code of Conduct

[TODO: Depoda `CODE_OF_CONDUCT.md` dosyası bulunmuyor.]

<!-- FAQ -->
## :grey_question: FAQ

- Termal veriler gerçek NASA ölçümleri mi?

  + Hayır. `thermal_grid.py` yüzey sıcaklığını DEM'den sentetik olarak üretir: yükseklikten temel sıcaklık (−180 °C ile +80 °C), bakıya göre güneşlenme düzeltmesi ve kuzey komşusunun yüksekliğine dayalı yerel gölge cezası. Ay güney kutbu için makul bir yaklaşımdır ancak ölçüm verisi değildir. Gölge oranı da benzer şekilde yüksekliğe dayalı bir vekildir, ışın izleme ile hesaplanmaz.

- `/api/plan` neden `503` dönüyor?

  + Izgaralar yüklenmemiş. Önce veri hattını çalıştırıp `POST /api/load-preprocessed` çağırın veya `backend/data/dem/` altındaki bir DEM için `POST /api/load-dem` kullanın. Backend açılışta `lunapath/data/processed/` klasörünü kontrol eder; dosyalar yoksa uyarı verip veri olmadan başlar.

- Başlangıç veya hedef noktası seçince `422` alıyorum, neden?

  + Seçilen hücre o rover için geçilemez durumda. Bir hücre, eğimi rover'ın `slope_max_deg` sınırını aşarsa, yüzey sıcaklığı −150 °C'nin altındaysa ya da veri `NaN` içeriyorsa engelli sayılır. Rover değiştirmek eşikleri de değiştirir: NASA VIPER için sınır 20°, LPR-1 için 25°'dir. Traverse katmanına geçip geçilebilir bir bölge seçin.

- Hangi DEM dosyası gerekiyor ve neden depoda yok?

  + `LDEM_80S_80MPP_ADJ.tiff` (NASA LRO/LOLA, Ay güney kutbu, 80 m/piksel). Dosya boyutu nedeniyle `.gitignore` ile hariç tutulmuştur; `*.tif`, `*.tiff`, `*.img` ve `*.npy` uzantıları ile `data/raw/`, `data/processed/` klasörleri sürüm kontrolüne dahil edilmez.

- Ağırlıkları değiştirdiğimde tüm veri hattını yeniden çalıştırmam gerekir mi?

  + Gerekmez. Maliyet ızgarası ağırlıklar değiştiğinde bellekte yeniden hesaplanır (500 × 500 için saniyenin altında). Yalnızca eğim, bakı veya termal katmanların kendisi değişirse hattı yeniden çalıştırmak gerekir.

- Aynı anda birden fazla rover ile rota planlanabilir mi?

  + Hayır, bir rota için tek rover kullanılır. Ancak `/api/plan-multi` ve `/api/compare` uçları aynı rover ile farklı görev profillerini karşılaştırmalı olarak planlar.

<!-- License -->
## :warning: License

Distributed under the Apache License 2.0. See `LICENSE` for more information.

Copyright 2026 Ahmet Karakoyun, Nedim Göktuğ Tabak, Tuna Deniz, Oğuzhan Tarhan, İzzettin Berke Kuş.

<!-- Contact -->
## :handshake: Contact

Proje ekibi: Ahmet Karakoyun, Nedim Göktuğ Tabak, Tuna Deniz, Oğuzhan Tarhan, İzzettin Berke Kuş

Proje bağlantısı: [https://github.com/feza-co/TUAASTROHackathon](https://github.com/feza-co/TUAASTROHackathon)

Soru ve hata bildirimi: [https://github.com/feza-co/TUAASTROHackathon/issues](https://github.com/feza-co/TUAASTROHackathon/issues)

[TODO: Ekip için genel bir iletişim adresi veya sosyal medya hesabı belirtilmemiş.]

Ek teknik belgeler:

- [docs/lunapath_referans_belgesi_2.md](docs/lunapath_referans_belgesi_2.md) — formüller, sabitler, maliyet modeli
- [docs/ay_termal_navigasyon_proje_dokumani.md](docs/ay_termal_navigasyon_proje_dokumani.md) — proje dokümanı
- [docs/lunar_data_thermal_team_docs.md](docs/lunar_data_thermal_team_docs.md) — veri ve termal ekip notları
- [docs/stitch_design_brief.md](docs/stitch_design_brief.md) — arayüz tasarım notları
- [docs/lunar_report_markdown/lunar_data_preprocessing_report.md](docs/lunar_report_markdown/lunar_data_preprocessing_report.md) — ön işleme raporu

<!-- Acknowledgments -->
## :gem: Acknowledgements

 - [Shields.io](https://shields.io/)
 - [Awesome README](https://github.com/matiassingers/awesome-readme)
 - [Emoji Cheat Sheet](https://github.com/ikatyang/emoji-cheat-sheet/blob/master/README.md#travel--places)
 - [Readme Template](https://github.com/othneildrew/Best-README-Template)
 - NASA LRO / LOLA — `LDEM_80S_80MPP_ADJ` Ay güney kutbu sayısal yükseklik modeli
 - NASA LRO / LROC WAC Global Mosaic — 3D karşılama sahnesindeki Ay dokusu (`moon-lroc-wac-global-1024.jpg`)
 - Türkiye Uzay Ajansı (TUA) ASTRO Hackathon — projenin geliştirildiği etkinlik

[TODO: Yukarıdaki veri kaynakları için resmi bağlantılar ve tam atıf metinleri eklenmeli.]

---

*Hackathon / demo amaçlıdır; gerçek görev analizi yerine geçmez. Uzay verilerinin lisans ve kullanım koşullarına uygun kullanın.*
