# About bruno
In early 2022, Aaron told me (with excited voice) that he came up with a new card game, which is based on [<u>br</u>idge](https://en.wikipedia.org/wiki/Contract_bridge) and [<u>UNO</u>](https://en.wikipedia.org/wiki/Uno_(card_game)). I was persuaded to try it out and actually found it interestering. Later we thought why not writting an application so that everyone who are interested can play it online. This repository is an implementation of the game. In a hypothetical but implausible future, we want to build a reinforcement learning agent to play this game, with the hope that it can achieve similar or better performance than human players.

# Game settings
***Players and Teams***:
The game involves 4 players who take turns to play cards. Players who are not adjacent, in terms of the play order, belong to the same team. For example, if the play order is A → B → C → D, then A&C belong to one team, B&D another.

***Cards distribution***: Each player will be randomly assigned 13 cards at the beginning of the game
- 6 table cards:
    - 3 hidden cards: invisible to everyone, including the owner, adding randomness to the game
    - 3 shown cards: visible to everyone
- 7 hand cards: only visible to the owner

***Objective***: The first player who played all 13 cards (both hand and table cards) wins the game for their team.


# Cards and Gameplay
***Card types***: The deck consists of 52 cards: 2/3/4/5/6/7/8/9/10/J/Q/K/A, each with 4 copies.
- **Ordinary cards**: 4-8, J-A in ascending order
- **function cards**: 2,3,9,10, with special effects
    - 2: Skips your turn (the next player will deal with the last played card)
    - 3: Skips you and the next player's turn (your teammate will deal with the last played card)
    - 9: Forces the next player to play a card smaller than 9.
    - 10: Collects all hand cards, shuffles them, and redistributes to players by the play order, with the current player receiving the first card. After re-distribution, the next player will deal with the last played card. (The used 10 is excluded from the rest of the game, meaning they will not be collected to players' hand once it's played.)
    
***Gameplay***: 
1. Playing rules
    - The first player starts their round by playing any card. Following players must play cards greater or equal to the last played card or play function cards.
    - A player may play one card a time, or play multiple cards if these cards share the same value.
    - If a player has valid cards to play, they must play them. If a player has no valid cards to play, they must collect all the played cards to their hand.
    - The last card played to win the game cannot be a function card. If the last card (either hidden or hand card) is a function card, the player must collect all previously played cards into their hand.


2. Using Table and Hidden Cards
    - Once hand cards are depleted, players may choose 1 shown table cards to play.
    - If a player runs out of shown table cards, they can choose 1 hidden card to play.
    - If the chosen table card violate the playing rules, the player must collect all previously played cards into their hand.


3. Resetting the Round
    - If a player collects all the previously played cards, they may play any card to start a new round.

<hr>
<details>
<summary>
# 中文规则点这里
</summary>
一副去掉两张Joker的扑克牌，52张

四名玩家围坐，互相对面的是一队，逆时针依次出牌，谁先出光自己所有的牌，这一队就能获胜。

每名玩家拥有三种牌，桌面上的暗牌，桌面上的明牌，手牌。 最开始，向每个玩家派发3张桌面暗牌，3张桌面明牌，剩下的都是手牌。游戏开始，出牌的规则有：

1. 除非是第一个出牌，或者是游戏重置后第一个出牌，你的出牌的数字都必须大于等于上一家出的牌。
2. 有四张功能牌，分别是2，3，9，10。2是跳过自己的出牌回合，3是跳过自己和下一家的出牌回合，跳过回合意味着下一个出牌的人要应对你本该应对的牌，9会要求下一家出小于9的牌，10会收集所有玩家的手牌并且 洗牌重新均匀发给大家，而打出的10会被排除在游戏外，之后由你的下家来应对你本该应对的牌。这四种功能牌可以在任意你的回合出，也就是不受上一家出牌限制。
3. 如果没有不小于上一家出牌的普通牌，也没有功能牌，那么就要收回场上所有的牌，并且游戏重置，你再出一张牌来开始新的一回合。
4. 必须出完手牌，才能出桌面上的明牌；必须出完桌面上的明牌，才能出桌面上的暗牌，因为你不知道暗牌是什么，所以你是任意挑选一张，翻开，然后判定出牌是否符合上述规则，如果不符合，比如说你翻开的暗牌不是 功能牌，又比上一家出牌要小，那你就要回收场上所有的牌，如规则3。
5. 所有的手牌和桌面上的明牌，在出牌时数量和花色都不重要，比如说上家出了一个黑桃4，你可以一起出方片4和梅花4，或者说上家出了两张，你可以接一张。
6. 在获胜之前，也就是打出最后一张牌时，你不能打出功能牌。如果最后一张是功能牌，那你就需要收回场上所有的牌，然后如规则3。
</details>
