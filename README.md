# About Online Chess Cheating

In 2020, CHESS.com saw its popularity grow in astronomic ways.
This happened mostly due to the recent ascension of the Netflix show The Queen's Gambit, with other events like the COVID-19 pandemic and [GM Hikaru Nakamura’s](https://en.wikipedia.org/wiki/Hikaru_Nakamura) Twitch.tv channel substantial growth in the last year.
This player expansion was, in general, very beneficial to the chess community overall, however, it ended up being a double-edged sword in the long run.

In August 2020, the website’s anti-cheat team compiled in a [single article](https://www.chess.com/article/view/online-chess-cheating) some metrics about the account bans and how this process works.
This article has the objective to validate the methods presented in the CHESS.com text and to try, in a more sophisticated way, to use one of the most common cheats in chess: The Engines.

Before we go on, it’s good to highlight that the use of Engines in CHESS.com is strictly prohibited according to the [fair-play policy](https://support.chess.com/article/648-what-do-i-need-to-know-about-fair-play-on-chess-com) of the website.
The matches shown in this article were previously agreed with the opponents and the objective of this text is merely informative and educational.

## About Engines

In a general manner, an Engine, when talking about chess, is a computer software capable of evaluating positions in a chess game.
The software can achieve that goal calculating each possible play in each round, taking in consideration some important variables like most active pieces, the king’s position, pawn structure, amount of material, etc.

The magic happens in the moment that this process repeats itself, meaning that the computer does the calculation for the first possible move, to the second possible move, all the way to the supposedly last move.
In each of the possible moves it will repeat the process, this way, creating an infinite amount of chess games, testing each single possibility.
Only after all this calculation process the computer can suggest which is the single best move to do in that situation.

Unfortunately, all the computing power available in the entire world is not enough to calculate a complete chess game, instead of this, the Engines work with a depth system.
The [Stockfish Engine](https://stockfishchess.org/), available at CHESS.com for example, analyzes the plays in a depth of 18 recursions [enough to reach a FIDE rating of 2761](http://web.ist.utl.pt/diogo.ferreira/papers/ferreira13impact.pdf).

## How Engines are detected

The most common way to detect a player that is cheating is the accuracy of his moves.
The use of an Engine like Stockfish or [Komodo](https://komodochess.com/) will result in a literal perfect game in the side of the cheater, with zero mistakes or imprecisions – something that is almost impossible to achieve even for the elite players.

Another point that should be looked up into is the time that the players take to do each one of their movements.
When you use a software like that, there is a delay – usually constant – when the calculations of the best possible move happen, only after that delay time the player can make the move.

There are also some external factors, like the date when the account was created, the number of matches, the rating evolution, etc.

Therefore, if you face a player that moves in a constant way, that has recently created his account or played only a few matches, and besides that, plays in a similar way as the [GM Fabiano Caruana](https://en.wikipedia.org/wiki/Fabiano_Caruana), be suspicious, he probably is using an Engine against you.

## How to hinder the detection of an Engine

Using the section above as a basis, we can deduct some methods that can hinder the CHESS.com methods of Engine detection.
The first matter is not using an elite software like Stockfish or Komodo, instead of that, choose something worst or Engines that offer some method of creating a personality in the game style, like the [Rodent_III](https://github.com/nescitus/Rodent_III) for example.

Other factor to take in consideration is the time of each move, if you move in a constant way you will be rapidly punished.
A way of avoiding that punishment is playing the opening in a quicker way, while taking a longer and more dynamic time in the midgame, going back to the fast moves in the endgame or in case of shortage in time.

By strictly following these two tips you should avoid any type of punishment in your account for a while, however it is inconvenient for a human being to follow these rules in such a precise way, so we will see ahead a way of merging all this process to CHESS.com itself, fully automated and with the Engine playing literally alone.

## CHESS.com Methods

Just like most of the browser multiplayer games, CHESS.com uses a real-time message exchange protocol.
In a simpler way: you, Player A, make a move, the CHESS.com will receive your move and update Player’s B board, your opponent.
Then, Player B will respond the move, that way CHESS.com will receive his response and update your board.

With the move exchange dynamic described above, it is possible to think of a few ways to automate the game.
Here we will modify CHESS.com source code to open a giant number of possibilities that will start from intercepting the match moves all the way to making a connection with an Engine.

Fortunately, CHESS.com has a few security barriers to avoid that kind of modification – nothing that a person with a lot of free time cannot solve.
Being simple, each play made on the website is encrypted with an algorithm of their own called TCN, the move “1. e4” for example, is converted into “mC”, the move “2. e6” is converted into “0S” and so on.
That way, CHESS.com makes it impossible to send moves to the server that were not originated from the website itself.
However, after a little bit of reverse engineering, its possible to isolate the code that is responsible for this encrypting. He is also available at [GitHub](https://github.com/omppye-tech/chess-tcn).

## New movement flow

After the changes, the flow of a common game has changed to: You, Player B, will get your movement from your opponent, the modification in the CHESS.com code detects the move and calculate, together with an Engine, which will be the best response, after that, it will make the move and send it back to your opponent.
With that, we can add a few time checks in this same code to make it harder for your engine to get detected, for example:

1. If the player is between move 1 and move 32, consider as the beginning of the game and play faster.
2. If the player is after move 32 and has more than 40 seconds of left game time, consider as the midgame, and play in a more slow and dynamic way.
3. If the player has less than 40 seconds of left game time, consider as endgame or time shortage and play in a quicker way.

## Results

Until this moment we were only theorizing, but the software above was really built.
He embraces all that was mentioned and utilizes an open Engine called [Rodent_III](https://github.com/nescitus/Rodent_III), due to its customization in game style.
In case you have any questions regarding this text or more in-depth techniques I am open to receiving messages in my Discord account `omppye#0001`.
Therefore, this project source code is also available at [GitHub](https://github.com/omppye-tech/bran) and the demonstration is on [YouTube](https://www.youtube.com/watch?v=MlTHEjqT8eU)

Thank you!

## License

This project is distributed under the [MIT license](LICENSE)
