# Game of War: Strategy Board Game

A 2D hidden-rank war strategy board game on a 10×10 field, in the style of Game of the Generals (Salpakan), with a few twists: barricades, a one-shot air strike, 12 roaming power-ups and 2 hidden land mines.

**Play it:** https://spacecarl9001.github.io/Game-of-War/

## Ways to play

- **Online with a friend:** one player taps **Create online game** and shares the room code or invite link; the other taps **Join or watch online**, enters the code and taps **Join** (or just opens the link). Both deploy at the same time on a shared 90-second clock.
- **Watch an online game:** anyone with the room code can tap **Join or watch online**, enter the code and tap **Watch**, before or during the battle (up to 8 spectators). Spectators see both sides' ranks and kill counts, including both formations during deployment; the hidden mines and each player's private battle reports are shown only when the battle ends. They keep watching through a rematch. Spectators can't react or send messages during the game, but they see both players' reactions. Both players see how many people are watching (hover for names).
- **Against the computer:** works offline, at three levels:
  - **Easy:** plays by simple habits.
  - **Normal** and **Hard:** keep a belief about every enemy piece's rank built only from what a player can see (the battles it fought against which of its own ranks, where it started, whether it moved or attacked, its power-ups and kills), score every move by expected value, guard and hide their flag with decoys, and save the air strike for a confident shot at your flag. Hard plays sharper and takes fewer chances. Neither ever looks at your hidden ranks or the mine positions.

  - **Expert:** Hard's judgement plus:
    - a look one move ahead for both sides: your strongest reply against its own best recapture and follow-up attack
    - hiding its flag: it tracks what you can work out from public facts (who moved, attacked or survived a battle) and avoids moves that give the flag away
    - barricades placed to block the shortest roads to its flag and its back row
    - running its own flag down open lanes, and chasing any piece of yours that might be your flag heading for its back row
    - firing its air strike sooner when it thinks you're close to finding its flag

    It plays by the same fair-play rule and never sees your ranks or the mines.

  In computer-vs-computer test matches (100 games each), Hard beat Easy 96–2 and Normal 60–31, and Normal beat Easy 69–27. Expert won 75.5% of 440 games against Hard.
- **Pass and play:** two players on one phone, with a hand-off screen between turns. Works offline.

Before every game, each player types their name (the last names used are filled in). Names replace "Ivory" and "Onyx" in the turn indicator, hand-off screens, field log and result screen. Online, the host enters theirs when creating the room and the guest on the join screen.

Also on that screen:

- **Time control** (optional): Off, or 3, 5 or 10 minutes per player with +3 seconds after every move, like a chess clock. Only the side to move loses time, and running out loses the game. The clock pauses on pass-and-play hand-off screens and while an online connection is down; online, the host's clock is the official one.

During a game:

- **Pre-moves:** against the computer or online, queue your next move during the enemy's turn (tap a piece, then a square). It plays the moment your turn starts if it's still possible, otherwise it's cancelled. Can be switched off in the orders panel.
- **React:** send an emoji or a short taunt ("Is that all?", "GG"…) that pops up over the board for both players. The computer reacts too. You can hide your opponent's reactions.
- **Chat (online):** type messages to your opponent in the Chat box under your orders. Their messages also pop up over the board. Chat is only between the two players: spectators can't read or send messages. You can hide your opponent's messages, and reconnecting to the same game keeps the conversation.

## Install on a phone

Open https://spacecarl9001.github.io/Game-of-War/ on your phone, then:

- **Android (Chrome):** ⋮ menu → **Install app**
- **iPhone (Safari):** Share → **Add to Home Screen**

It runs full screen with its own icon, works offline after the first load (online games still need internet), and saves an offline game in progress if the phone closes the app.

## How online play works

The two phones connect directly to each other (WebRTC). [PeerJS](https://peerjs.com)'s free public service only introduces them; the game itself does not go through a server. The player who creates the room hosts the game: their phone runs the rules and sends the guest only what the guest is allowed to see, so enemy ranks and mine positions never reach the guest's phone. Spectators connect to the host the same way and get both sides' ranks, but never the mine positions before the battle ends. If either side drops, the game pauses and the guest can reconnect with the same code while the host keeps the app open.

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
