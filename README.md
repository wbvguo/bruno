In early 2022, Aaron got an idea of a new card game, which is originated from [bridge](https://en.wikipedia.org/wiki/Contract_bridge) and another popular broad game (name put here with link). Later we thought why not writting an application about it so that everyone who are interested can play it online. This repository is an implementation of the game. In the longrun, we want to develop a reinforcement learning based AI that can play this game, with the hope that it can achieve a similar or better level of human players.

# Rules
## Game settings
- Similar to bridge, there are 4 players in the game and they take turns to play. Players that are not adjecent, in terms of the order of play, belongs to the same team. For example, if play order is A,B,C,D, then player A&C belong to one team, B&D another.
- Each player will have 6 table cards (3 hidden and 3 shown. The hidden cards are invisible to anyone (including the owner) and is the major source of randomness. The shown cards are visible to everyone. Besides, each player will have 7 hand cards, which is only visible to the owner.
- After playing, we will have a player who first play all the 13 cards (both hand and table cards) out. The team who has that player wins the game.

## Cards & playing
- There are 52 cards in total (2/3/4/5/6/7/8/9/10/J/Q/K/A, each with 4 copies).
- 4-8, J-A are ordinary cards, sorted from smaller to bigger.
- 2,3,9,10 are functional cards.
	- 2: skip the current round of play (next player will start his/her round)
	- 3: skip the next round of play (teammate will start his/her round)
	- 9: the next player can only play a card that is smaller or equal to 9
	- 10: shuffle the hand cards and re-distribute to players by the current playing order (the player will recive the first card)
- Each player must play a euqal or bigger card than the previous card or play a function card.
- Each player only allows to play one card at a round. But if you have duplicate cards, you can play all of them in one round.
- If you have card option for playing, you must play. If you don't have a card option for playing, collect all the played cards to your hand.
- If you run out of hand cards, you can play shown table cards. If you run out of shown table cards and hand cards, you can choose 1 hidden cards to play.
- If the hidden card cannot satisfy the previous card's requirement, then collect all the played cards to hand. 
- The last hand or table card cannot be a functional card, otherwise, collect all the played cards to your hand.
- If the former player collect all the played cards to hand, the current player can play any cards.

