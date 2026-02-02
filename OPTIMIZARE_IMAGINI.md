# Optimizare Imagini - Best Practices

## 1. **Optimizare Locală (Recomandat pentru început)**

### Comprimare Imagini
- **Tool**: ImageOptim, TinyPNG, Squoosh
- **Rezultat**: Reducere 60-80% din dimensiune
- **Format**: WebP (fallback la JPG pentru browsere vechi)

### Thumbnails pentru Galerie
- **Dimensiuni recomandate**:
  - Thumbnail: 300x300px (pentru grid)
  - Medium: 800x600px (pentru lightbox)
  - Full: Original (pentru download)

## 2. **Hosting Static cu CDN (Recomandat)**

### Opțiuni:
- **Netlify**: CDN inclus, optimizare automată
- **Vercel**: Optimizare imagini automată
- **GitHub Pages + Cloudflare**: CDN gratuit

### Avantaje:
- ✅ CDN global (încărcare rapidă)
- ✅ Optimizare automată
- ✅ HTTPS inclus
- ✅ Scalabil

## 3. **Cloud Storage (Pentru site-uri mari)**

### AWS S3 + CloudFront
```
images/
  ├── thumbnails/ (300x300)
  ├── medium/ (800x600)
  └── full/ (original)
```

### Cloudinary / ImageKit
- Optimizare on-the-fly
- Transformări dinamice
- CDN inclus
- **Cost**: ~$0.01/GB storage + $0.01/GB transfer

## 4. **Implementare Recomandată pentru VeraMob**

### Faza 1: Optimizare Locală (ACUM)
1. Comprimare poze existente (TinyPNG)
2. Conversie la WebP
3. Generare thumbnails

### Faza 2: Hosting (VIITOR)
1. Deploy pe Netlify/Vercel
2. CDN automat
3. Optimizare continuă

### Faza 3: Cloud Storage (DACĂ crește traficul)
1. Migrare la Cloudinary
2. Optimizare on-the-fly
3. Analytics imagini

## 5. **Structură Recomandată**

```
images/
  ├── thumbnails/
  │   ├── Bucatarii/
  │   ├── Sufragerii/
  │   └── ...
  ├── medium/
  │   ├── Bucatarii/
  │   └── ...
  └── full/
      ├── Bucatarii/
      └── ...
```

## 6. **Cod Exemplu - Responsive Images**

```html
<!-- Modern approach -->
<picture>
  <source srcset="images/hero.webp" type="image/webp">
  <source srcset="images/hero.jpg" type="image/jpeg">
  <img src="images/hero.jpg" alt="Hero" loading="lazy">
</picture>

<!-- With srcset for different sizes -->
<img 
  srcset="
    images/hero-small.jpg 480w,
    images/hero-medium.jpg 768w,
    images/hero-large.jpg 1200w
  "
  sizes="(max-width: 480px) 100vw, (max-width: 768px) 50vw, 33vw"
  src="images/hero-medium.jpg"
  alt="Hero"
  loading="lazy"
>
```

## 7. **Tool-uri Recomandate**

### Desktop:
- **ImageOptim** (Mac) - Comprimare automată
- **FileOptimizer** (Windows) - Batch processing
- **Squoosh** (Web) - Conversie WebP

### Online:
- **TinyPNG** - Comprimare JPG/PNG
- **Cloudinary** - Optimizare + CDN
- **ImageKit** - CDN + optimizare

## 8. **Metrici de Performanță**

### Obiective:
- ✅ Poze < 200KB (pentru web)
- ✅ Thumbnails < 50KB
- ✅ Lazy loading activat
- ✅ WebP support
- ✅ CDN pentru distribuție globală

### Verificare:
- Google PageSpeed Insights
- Lighthouse (Chrome DevTools)
- WebPageTest
