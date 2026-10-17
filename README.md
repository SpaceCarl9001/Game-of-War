# Game of the Generals

Salpakan on a 10×10 field, with a few twists: barricades, a one-shot air strike, 12 roaming power-ups and 2 hidden land mines. Play the computer, or pass one phone between two players.

## Play and install

Open the game's GitHub Pages link on your phone, then:

- **Android (Chrome):** ⋮ menu → **Install app**
- **iPhone (Safari):** Share → **Add to Home Screen**

It runs full screen with its own icon, works offline after the first load, and saves a game in progress if the phone closes the app.

## Run it locally

```
npm start
```

Then open http://localhost:5174. Phones on the same Wi-Fi can use `http://<this PC's IP>:5174` to play (installing needs the https GitHub Pages link).

## Files

- `index.html`: the whole game (rules, board, computer opponent)
- `manifest.webmanifest`: app name, icon and full-screen settings for installing
- `sw.js`: offline support. Change `VERSION` whenever the game changes so installed copies update.
- `icons/`: app icons

## Rules in short

- 21 pieces each, set up in your first 3 rows within 90 seconds.
- Higher rank wins a battle; equal ranks both fall. The Spy beats Sergeant and up but loses to a Private. Ranks stay hidden; you only learn if you won or lost.
- Win by capturing the enemy flag, by reaching the enemy's back row with your flag, or by hitting the flag with your air strike.
- Barricades: 2 horizontal and 2 vertical per side, one per turn, built before you move.
- Power-ups promote the winner of a battle fought on them, and jump to new squares after every turn.
- Land mines hide in rows 4–7 and destroy whatever steps on them.
