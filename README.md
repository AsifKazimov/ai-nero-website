# AI Nero ERP — təqdimat saytı

Statik sayt (build addımı yoxdur). Dillər: AZ / EN / RU. Ünvan: https://aineroerp.online/

## Fayllar

| Fayl | Nə üçün |
|---|---|
| `index.html` | Bütün sayt (CSS, JS, modul məlumatı `<script id="productData">`-da) |
| `guides/*.pdf` | Modul bələdçiləri (şirkət adları AA, BB, CC... ilə əvəz edilib) |
| `og-image.png` | Sosial şəbəkə önizləməsi (1200x630) |
| `sitemap.xml`, `robots.txt` | Axtarış sistemləri üçün (`/guides/` indekslənmir) |
| `CNAME` | GitHub Pages-də `aineroerp.online` domeni |
| `.nojekyll` | GitHub Pages-in Jekyll emalını söndürür |

## GitHub Pages-də yayımlamaq

1. Bütün faylları və `guides/` qovluğunu repo-nun KÖKÜNə yüklə (köhnə `index.html`-i əvəz et). `CNAME` olmasa domen hər yükləmədə sıfırlanır.
2. Settings → Pages → Source: `Deploy from a branch`, Branch: `main` / `(root)`.
3. Custom domain: `aineroerp.online` (CNAME faylı onu avtomatik yazır). `Enforce HTTPS` qutusunu işarələ.
4. DNS: `aineroerp.online` üçün GitHub Pages A qeydləri (185.199.108.153, 185.199.109.153, 185.199.110.153, 185.199.111.153); `www` üçün `<istifadəçi>.github.io`-ya CNAME.

## Məzmunu dəyişmək

- Modullar, alt bölmələr, sənəd növləri, addımlar: `productData` JSON-u (hər sahə `az/en/ru`).
- İnterfeys mətnləri: `ui` obyekti (`az`, `en`, `ru` açarları, `data-t` atributu ilə bağlıdır).
- Bələdçi kartları: `<section id="guides">`; mətnlər `ui`-da `g1t..g6d` açarlarıdır.
- `sitemap.xml`-də `lastmod`-u kontent dəyişəndə yenilə.

## 01 Kadr bələdçisi — backend ilə tutuşdurulub (09.10.2026)

Kart aktivdir (`guides/01-kadr-emekhaqqi.pdf`). Əvvəlki PDF-dəki rəqəmlər ERP kodu ilə uyğun deyildi; 4 səhifə düzəldilib (qalan 13 səhifə toxunulmayıb):

| Səh. | Nə səhv idi | İndi (mənbə: ERP `payroll.service.ts`, `seed.ts` → `TaxRateConfig`) |
|---|---|---|
| 2 | Mündəricatda səhifə nömrələri 3-25 idi (PDF 17 səhifədir), mövcud olmayan bölmələr vardı (2.3 T-1/T-6/T-8, 2.5, 5.2, 6.3, Keys 3) | Real başlıqlar və real səhifələr |
| 13 | Gəlir vergisi "8000 ₼-dək 0%"; İTS "8000-dən yuxarı 1%"; işəgötürən DSMF-in 8000-dən yuxarı 11% pilləsi yox | Baza `Gross − 200`; 2500-dək 3% (2027: 5%, 2028: 7%), 2500-8000: 75 + 10%, 8000+: 625 + 14%. İTS: ilk 2500 → 2%, qalanı 0.5%. DSMF işəgötürən: 22% / 44 + 15% / 1214 + 11% |
| 14 | Kt 522.1/522.2/522.3 (hesablar planında yoxdur), maya zənciri "Dt 204.1 / Kt 771" | Kt 522; Dt 202 / Kt 771.x → Dt 204.1 / Kt 202 (`mrp.service.ts`). 771.1 seçimi T-1 əmrindəki «Xərc Hesabı» ilədir (defolt 721). Keys 1-in provodka cədvəli əlavə olunub |
| 17 | Keys 1: Net 1,414.00 ₼ (gəlir vergisi 0%); FAQ 1: "sistem 721-i bloklayır" | Net **1,372.00 ₼** (gəlir vergisi 42.00); sistem bloklamır — xərc kartdakı hesaba gedir |

Yoxlama: Şəkil 4.2-dəki ekran (2027-08 dövrü, ilk pillə 5%) eyni düsturla 1,344.00 / 1,261.50 / 849.00 verir — ekrandakı rəqəmlərlə üst-üstə düşür. Mühasibin təsdiqlədiyi 1,000 ₼ → 865.00 ₼ nümunəsi səh. 14-dədir.

## Qeydlər

- "Nəzarət qaydaları" bölməsindəki 6 qaydanın hamısı backend kodunda təsdiqlənib. Yeni qayda əlavə edəndə əvvəl kodda yoxlayın.
- Vergi dərəcələri, hesab kodları və provodka zəncirləri saytın mətnində göstərilmir. Bələdçilərdə isə nümunə kimi var, buna görə səhifədə xəbərdarlıq qeydi saxlanılıb.
- `productData`-dakı `status: "implemented"` sahəsi səhifədə göstərilmir; real vəziyyət üçün ERP repo-sundakı `VEZIYYET.md`-ə baxın.
- Bələdçi PDF-lərində işçi adları və FİN-lər hələ də görünür (yalnız şirkət adları maskalanıb).
