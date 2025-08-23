Unity Intern Test
Task 1: Re-skin

Go to the prefab folder and replace all item sprites with fish sprites.

Task 2: Game Feature Implementation
Step 1: Create Bottom Row Object

Create a new class BottomRow.
Assign its transform and configure its settings inside GameSettings.
In GameSettings, add a new parameter: bottomCellSize.


Step 2: Disable Item Dragging on the Board

In BoardController, comment out (or disable) all methods related to item movement/interaction such as:
Hint
Collapse
ShiftDown
… and any other similar functions.
Purpose: Items should only spawn once and cannot interact with each other.



Step 3: Add Features to Bottom Cell

Implement the following functions inside BottomCell:
AddToBottom: Handle logic when an item is selected and moved into the bottom row.
CheckMatch: Check if items in the bottom row match. If yes → remove them and shift the remaining items to the left.
ShiftLeft: Shift items left if there are empty spaces.
ShiftRight: If a new item from the board matches one already in the bottom row, insert it and push other items to the right.
CheckEmptyItem / CheckFullItem:Check whether the bottom row still has free space.If the row is full → trigger the Lose condition.


Step 4: Adjust Gameplay Rules
Board size: Change rows and columns to 6x6 for balance and to ensure enough item types.
Spawn rule:
Replace the old spawn logic with a new one:
Each item type must spawn in multiples of 3 (e.g. 3, 6, 9, …).
First, spawn 3 of each type.
Then, spawn the remaining items randomly, ensuring the total count of each type is divisible by 3.
After spawning → run the existing Shuffle() function to randomize.



Step 5: Auto Win / Auto Lose Features

AutoWin: Automatically pick matching items until all are cleared.
AutoLose: Automatically pick non-matching items until the bottom row is full and no matches are possible.
GameManager changes:

Add public GetLevelType() to customize gameplay for different modes.
Move Mode: Lose if the bottom row is full. Items cannot be added back once placed.
Time Mode: The game continues even if the bottom row is full. Items can still be added.
Update BoardController input handling to respect these conditions.

UI changes:
In UIPanelGame, add two new buttons: Auto Win and Auto Lose.
Subscribe their events to trigger AutoWin() and AutoLose() in UIManager → GameManager.


Step 6: Display Win / Lose States

Add new game states: Win and Lose.
Initially, only Win screen is shown on game end → split them into two states.

In GameManager:
Add a state parameter for WaitBoardController.
Add a state parameter for OnConditionComplete in LevelCondition.
Create a new UI panel:
UIPanelGameWin → for win screen.
UIPanelGameOver → for lose screen.

Task 3: Separate Game Modes
Since the code is already optimized, just separate the modes into two different buttons.
Add a new button and assign it to Timer Mode.

When the timer runs out, the game state changes to Game Over (instead of default Win).

Animations:

Use DoTween for all item movement animations.
