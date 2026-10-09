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

## 01 Kadr bələdçisini aktivləşdirmək

Kart hazırda "Tezliklə" göstərir, çünki bələdçidəki gəlir vergisi cədvəli və Keys 1 hesablaması backend kodu ilə uyğun deyil (mühasib təsdiqi gözlənilir). Düzəldilmiş PDF-i `guides/01-kadr-emekhaqqi.pdf` adı ilə əlavə et və `index.html`-də 1-ci kartdakı
`<span class="outline-btn guide-soon" aria-disabled="true" data-t="guideSoon">Tezliklə</span>` sətrini
`<a class="outline-btn" href="guides/01-kadr-emekhaqqi.pdf" target="_blank" rel="noopener" data-t="guideOpen">PDF-ə bax ↗</a>` ilə əvəz et.

## Qeydlər

- "Nəzarət qaydaları" bölməsindəki 6 qaydanın hamısı backend kodunda təsdiqlənib. Yeni qayda əlavə edəndə əvvəl kodda yoxlayın.
- Vergi dərəcələri, hesab kodları və provodka zəncirləri saytın mətnində göstərilmir. Bələdçilərdə isə nümunə kimi var, buna görə səhifədə xəbərdarlıq qeydi saxlanılıb.
- `productData`-dakı `status: "implemented"` sahəsi səhifədə göstərilmir; real vəziyyət üçün ERP repo-sundakı `VEZIYYET.md`-ə baxın.
- Bələdçi PDF-lərində işçi adları və FİN-lər hələ də görünür (yalnız şirkət adları maskalanıb).
