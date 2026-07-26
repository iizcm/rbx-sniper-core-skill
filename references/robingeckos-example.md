# RobinGeckos — Concrete Example (project aktif setelah NeonHood)

## Konsep
- Nama: RobinGeckos (user pilih dr opsi "RobinGeckos aja")
- Tema: gecko/reptile cyberpunk streetwear, neon accents (pink #FF00FF / purple #9B30FF / cyan #00FFFF)
- **MAIN BG = Lime Green #CCFF00** (acuan baseline user utk semua project — karakter bs neon tp bg site = lime)
- Supply: 3333 (user set setelah negotiate; NeonHood 500, ini 3333)
- Chain: RBH 4663
- Tagline: "Cyberpunk Gecko Outlaws · Robinhood Chain"
- Bio mint card (user minta "lebih bagus dan keren"):
  "3333 cyberpunk geckos crawling the Robinhood Chain. Born from neon and streetwear — each one a degen outlaw with chrome tongue and glowing eyes. Freemint now, paid rounds soon. No roadmap. No promises. Just vibes and the neon green."

## Asset (WAJIB per project — rule locked)
- logo 500x500 (lime bg, clean gecko)
- banner 1500x500 (lime bg, gecko berkumpul)
- prereveal 500x500 (lime bg, glitch gecko)
- 10 char (lime bg + neon accents)
- Semua di /root/dl/ + http://134.199.170.183:8000/

## Website UX (LESSON PENTING — jgn copy-paste)
User marah: "UX jelek banget copy paste kaya website sebelumnya."
Referensi yg dipakai: rpad.fun (Robinpad launchpad) — style: card-grid, stats bar, mint card box.

Struktur final RobinGeckos (yg disetujui user):
- nav: logo + MINT/GALLERY/OPENSEA
- hero COMPACT: kiri teks (h1 + sub), kanan banner (gak huge full-width)
- stats bar: 4 kotak horizontal (Supply 3333 / Chain RBH 4663 / Network #CCFF00 / Status Mint Live)
- mint card: box (info h3 + bio + meta Supply/Freemint/Paid + button MINT NOW -> OpenSea)
- gallery: CARD GRID (border + caption per gecko, misal "VISOR #01")
- footer + floaty "GM DEGEN"

JANGAN: reuse HTML NeonHood mentah dgn ganti cuma teks/warna. Tiap project bikin layout yg reflect referensi user.

## Status (akhir sesi)
- ✅ 10 char + logo/banner/prereveal (lime bg) di /root/dl/
- ✅ website robingeckos_index.html (rpad-style) di /root/dl/
- ✅ neonhoodsite.vercel.app (NeonHood) masih live, tapi fokus pindah RobinGeckos
- ethers replay bug blm solved + primary habis (mint pending)
- next: deploy Vercel RobinGeckos / contract mint RobinGeckos
