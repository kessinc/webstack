# React ve Next.js İkon Kullanım Rehberi

Modern web projelerinde ikonlar, kullanıcı deneyimini (UX) zenginleştiren en önemli görsel öğelerdir. Bu rehberde, popüler kütüphaneleri kullanarak projelerinizi nasıl ikonlandıracağınızı öğreneceksiniz.

---

## 1. En Popüler İkon Kütüphaneleri

### A. React Icons (Hepsi Bir Arada)
`react-icons`, içinde Font Awesome, Material Design, Ant Design, Bootstrap Icons gibi 30'dan fazla ikon setini barındıran devasa bir pakettir.

**Kurulum:**
```bash
npm install react-icons
```

### B. Lucide React (Modern ve Hafif)
Özellikle modern, temiz ve tutarlı bir tasarım dili arayanlar için en iyi tercihtir. Tailwind CSS ile mükemmel uyum sağlar.

**Kurulum:**
```bash
npm install lucide-react
```

---

## 2. Temel Kullanım (React)

### React Icons Kullanımı
İkon setlerinin isimlerine göre klasörlerden import yapmanız gerekir:
- Font Awesome: `react-icons/fa`
- Material Design: `react-icons/md`
- Simple Icons (Sosyal Medya/Markalar): `react-icons/si`

```jsx
import { FaRocket } from 'react-icons/fa';
import { SiInstagram, SiFacebook } from 'react-icons/si';

function Header() {
  return (
    <div>
      <FaRocket size={30} color="blue" />
      <SiInstagram size={24} style={{ color: '#E4405F' }} />
      <SiFacebook size={24} style={{ color: '#1877F2' }} />
    </div>
  );
}
```

### Lucide React Kullanımı
```jsx
import { Camera, Heart, Settings } from 'lucide-react';

const Card = () => (
  <div className="flex gap-4">
    <Camera color="red" size={48} />
    <Heart fill="red" />
    <Settings className="animate-spin text-gray-500" />
  </div>
);
```

---

## 3. Next.js (App Router) ile İkon Kullanımı

Next.js 13+ ile gelen **App Router** yapısında, bileşenler varsayılan olarak **Server Component**'tir. İkon kütüphaneleri genellikle saf SVG döndürdüğü için Server Component'lerde sorunsuz çalışırlar.

### Performans İpucu (Tree Shaking)
İkonları import ederken sadece ihtiyacınız olanı çekmek paket boyutunu küçük tutar.

### Dinamik Renk ve Tailwind CSS
Next.js projelerinde Tailwind CSS kullanıyorsanız, ikonlara `className` üzerinden müdahale etmek en pratik yöntemdir:

```jsx
import { Mail } from 'lucide-react';

export default function ContactButton() {
  return (
    <button className="flex items-center gap-2 p-3 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition">
      <Mail className="w-5 h-5 text-white" />
      Bize Ulaşın
    </button>
  );
}
```

---

## 4. Sosyal Medya İkonları ve Markalar

Eğer Twitter (X), Instagram, Facebook gibi marka ikonlarına ihtiyacınız varsa `Simple Icons` (si) seti en güncel olanıdır.

| Marka | Import Yolu | Bileşen Adı |
| :--- | :--- | :--- |
| Instagram | `react-icons/si` | `SiInstagram` |
| Facebook | `react-icons/si` | `SiFacebook` |
| X (Twitter) | `react-icons/si` | `SiX` |
| LinkedIn | `react-icons/si` | `SiLinkedin` |
| TikTok | `react-icons/si` | `SiTiktok` |

---

## 5. İkonları Global Olarak Stilize Etme (React Icons Context)

Projenizdeki tüm ikonların aynı renk veya boyutta olmasını istiyorsanız `react-icons`'ın **Context API** desteğini kullanabilirsiniz.

```jsx
"use client"; // Next.js kullanıyorsanız ekleyin
import { IconContext } from "react-icons";
import { FaUser, FaLock } from "react-icons/fa";

export default function Layout({ children }) {
  return (
    <IconContext.Provider value={{ color: "blue", size: "1.5em", className: "global-icon" }}>
      {children}
    </IconContext.Provider>
  );
}
```

---

## 6. Özet ve Tavsiyeler

1.  **Hız ve Çeşitlilik:** `react-icons` kullanın. Arama yapmak için [react-icons.github.io](https://react-icons.github.io/react-icons/) sitesini kullanın.
2.  **Modern Görünüm:** `lucide-react` tercih edin. Özellikle admin panelleri ve modern UI'lar için idealdir.
3.  **Erişilebilirlik (A11y):** Eğer ikonun yanında açıklayıcı bir metin yoksa, ekran okuyucular için mutlaka `aria-label` ekleyin:
    - `<FaTrash aria-label="Sil" />`
4.  **Boyutlandırma:** İkon boyutlarını sabit tutmak için CSS sınıfları (`w-6 h-6` gibi) veya kütüphanenin `size` prop'unu kullanın.

