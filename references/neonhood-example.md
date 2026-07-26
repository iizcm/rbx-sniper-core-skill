# NeonHood — Concrete Degen NFT Launch Example

Reusable shape for "next RBH project" after Robin Hoodies died. User picks name, supply, freemint/paid split, theme color.

## Launch brief (user's final shape)
- Name: **NeonHood**
- Tagline: *Outlaws of the Neon Green*
- Supply: **2222** · **500 freemint** + 1722 paidmint ("hurry up")
- Chain: RBH (4663)
- Theme bg: **Lime Green #CCFF00** (Robinhood network color, dari foto user)
- NO roadmap, full degen
- Concept: cyberpunk/sci-fi outlaws (Robin Hood era digital), helm mekanis + visor nyala + circuit armor

## Asset pipeline (all via IAMHC image gen, parallel 9 key)
1. 10 char cyberpunk (traits: helm/visor/armor/jacket/mask/crown/hood/exo/scarf/core) -> expand later
2. Logo 500x500 (no text, no NFT title) — ffmpeg resize from 1024
3. Banner 1500x500 (chars gathered + "NEON HOOD" text via ffmpeg drawtext, DejaVuSans-Bold.ttf, boxcolor 0xCCFF00)
4. Prereveal 500x500 (mysterious hooded glitch silhouette, lime glow)
5. Website: Vercel deploy (`vercel deploy --prod --yes --token $VERCEL_TOKEN`), bg #CCFF00 + animated grid + glow, MINT NOW -> OpenSea

## 4 default shill posts (English, degen) — copy/edit per project
1. 🏹 PROJECT is LIVE on @Robinhood Chain / SUPPLY cyberpunk outlaws. LIME_GREEN_REBELS. 500 FREE MINT + PAID. No roadmap. Just vibes. 🌐 site 🔗 Mint: opensea.io #Tag #RBH #FreeMint #NFT
2. 💚 500 freemint gone fast. PAID after. Gas dirt cheap on RBH (~0.067 gwei). Don't sleep. 🌐 site #NFTCommunity #RobinhoodChain #Degen
3. ⚡ No roadmap. No promises. No BS. Just SUPPLY outlaws. You in or you poor? 🏹💚 🌐 site #PROJECT #Freemint #WAGMI
4. 🏹 Outlaws of the LIME_GREEN. Freemint live. Hurry up — 500 only. 🌐 site 🔗 opensea.io #PROJECT #RBH #NFTdrop #DeFi

## Prereveal item name/desc (template)
- Name: `PROJECT — Encrypted [???]`
- Desc: Sealed in the neon void. Identity encrypted until reveal. LIME circuit pulses through the dark — a Merry Man of the digital age, waiting to be unmasked. SUPPLY forged. FREEMINT free, PAID paid. No roadmap. Just vibes. 🏹💚

## Deploy result (this session)
- Site: https://neonhoodsite.vercel.app (alias https://neonhoodsite-fh8oewdvy-iizcms-projects.vercel.app)
- VPS download mirror: http://134.199.170.183:8000/ (neonhood_logo_500.png, neonhood_banner_1500x500.png, neonhood_prereveal_500.png, neonhood_chars/, neonhood_index.html)
