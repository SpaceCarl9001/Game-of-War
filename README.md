# Game of War: Strategy Board Game

A 2D hidden-rank war strategy board game on a 10×10 field, in the style of Game of the Generals (Salpakan), with a few twists: barricades, a one-shot air strike, 12 roaming power-ups and 2 hidden land mines.

**Play it:** https://spacecarl9001.github.io/Game-of-War/

## Ways to play

- **Online with a friend:** one player taps **Create online game** and shares the room code or invite link; the other taps **Join online game** (or just opens the link). Both deploy at the same time on a shared 90-second clock.
- **Against the computer:** works offline, at three levels:
  - **Easy:** plays by simple habits.
  - **Normal** and **Hard:** keep a belief about every enemy piece's rank built only from what a player can see (the battles it fought against which of its own ranks, where it started, whether it moved or attacked, its power-ups and kills), score every move by expected value, guard and hide their flag with decoys, and save the air strike for a confident shot at your flag. Hard plays sharper and takes fewer chances. Neither ever looks at your hidden ranks or the mine positions.

  In computer-vs-computer test matches (100 games each), Hard beat Easy 96–2 and Normal 60–31, and Normal beat Easy 69–27.
- **Pass and play:** two players on one phone, with a hand-off screen between turns. Works offline.

Before every game, each player types their name (the last names used are filled in). Names replace "Ivory" and "Onyx" in the turn indicator, hand-off screens, field log and result screen. Online, the host enters theirs when creating the room and the guest on the join screen.

## Install on a phone

Open https://spacecarl9001.github.io/Game-of-War/ on your phone, then:

- **Android (Chrome):** ⋮ menu → **Install app**
- **iPhone (Safari):** Share → **Add to Home Screen**

It runs full screen with its own icon, works offline after the first load (online games still need internet), and saves an offline game in progress if the phone closes the app.

## How online play works

The two phones connect directly to each other (WebRTC). [PeerJS](https://peerjs.com)'s free public service only introduces them; the game itself does not go through a server. The player who creates the room hosts the game: their phone runs the rules and sends the guest only what the guest is allowed to see, so enemy ranks and mine positions never reach the guest's phone. If either side drops, the game pauses and the guest can reconnect with the same code while the host keeps the app open.

## Run it locally

```
npm start
```

Then open http://localhost:5174. Phones on the same Wi-Fi can use `http://<this PC's IP>:5174` to play (installing needs the https GitHub Pages link).

## Files

- `index.html`: the whole game (rules, board, computer opponent, online play)
- `manifest.webmanifest`: app name, icon and full-screen settings for installing
- `sw.js`: offline support. Change `VERSION` whenever the game changes so installed copies update.
- `icons/`: app icons

## Rules in short

- 21 pieces each, set up in your first 3 rows within 90 seconds.
- Higher rank wins a battle; equal ranks both fall. The Spy beats Sergeant and up but loses to a Private. Ranks stay hidden; you only learn if you won or lost.
- Win by capturing the enemy flag, by reaching the enemy's back row with your flag, or by hitting the flag with your air strike.
- Barricades: 2 horizontal and 2 vertical per side, one per turn, built before you move.
- Air strike: once per game, destroys any enemy piece or one square of any barricade.
- Power-ups promote the winner of a battle fought on them, and jump to new squares after every turn.
- Veterans: every 3rd enemy a piece defeats in battle promotes it one rank, stacking with power-ups. A 5★ General or a Spy cannot rank up.
- Land mines hide in rows 4–7 and destroy whatever steps on them.
- Surrender: the Surrender button under your piece counts ends the battle at once (after a confirmation); your opponent wins.
