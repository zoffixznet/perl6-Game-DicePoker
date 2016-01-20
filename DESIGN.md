# DESIGN NOTES

## Overall goals

The initial implementation must allow to play the same type of the
[Dice Poker as is available in The Witcher game](http://witcher.wikia.com/wiki/Dice_poker_in_The_Witcher), except the dice
chances will be the perfectly fair.

A more distal goal is to add a variable "luck" parameter for each player that
will make it more (or less) likely for that player to draw winning hands
in the game. This goal suggests the original implementation of the dice should
consider the weighted set types provided by Perl 6.

## Object Tree

The implementation would consist of these objects:

    Game::DicePoker
        Game::DicePoker::Player
        Game::DicePoker::Game
            Game::DicePoker::Game::Pot
            Game::DicePoker::Game::Round

### `Game::DicePoker`

The main object that tracks players of the game as well as controls the progress
of individual Dice Poker games.  It's likely a good design objective to make
the players' states saved between each time the program is run, so the player's
record can be kept until they go utterly bankrupt.

The new players will start with some set amount of orens and persist until they
go bankrupt. It must be possible to easily reset the state of a player.

### `Game::DicePoker::Player`

An object representing a player. Tracks the name of the player, the number
of wins/losses since we "sat down" to play, and the amount of
[orens](http://witcher.wikia.com/wiki/Oren) they have.

    Game::DicePoker::Player
    Game::DicePoker::Game
        Game::DicePoker::Game::Pot
        Game::DicePoker::Game::Round
