Unity Intern Test
Task 1: Re-skin

Go to Prefabs.

Replace all item sprites with fish sprites.

Task 2: Core Features
Step 1: Bottom Row

Create a new class: BottomRow.

Configure its Transform.

In GameSettings, add a new variable: bottomCellSize.

Step 2: Disable Dragging on Board

In BoardController:

Comment out all functions related to item movement/interaction (e.g. Hint, Collapse, ShiftDown, …).

Goal: Items should spawn only once and remain static (no interaction with each other).

Step 3: Bottom Cell Features

AddToBottom: Handles selecting an item → moves it down into the bottom row.

CheckMatch:

If 3 or more items in the bottom row match → destroy them.

Remaining items shift left to fill empty spaces.

ShiftLeft: Push items left if there are gaps.

ShiftRight:

If a selected board item matches an item in the bottom row,

Insert it and push the other items to the right.

CheckEmptyItem / CheckFullItem:

Detect if bottom row is empty or full.

If full → trigger Lose condition.

Step 4: Gameplay Adjustments

Change board size to 6x6 for balance.

New Spawn function (replacing old one):

Each item type count must be divisible by 3.

Start by spawning 3 of each item type.

Randomly generate the rest.

Ensure total count per type is divisible by 3.

Shuffle the board using the provided Shuffle() function.

Step 5: Auto Win / Lose

AutoWin: Automatically select matching items until the board is cleared.

AutoLose: Automatically select mismatched items → bottom row fills up with non-matching items.

GameManager updates:

Add a public method: GetLevelType().

Used to customize gameplay by mode:

Move Mode:

Lose if bottom row is full.

Do not allow adding items back once they are dropped.

Time Mode:

Continue playing even if bottom row is full.

Allow adding items again.

UI Updates:

In UIPanelGame:

Add 2 new buttons → Auto Win & Auto Lose.

Subscribe them to events that trigger auto play modes.

In UIMainManager:

Add methods AutoWin() and AutoLose() → call corresponding methods in GameManager.

Step 6: Display Win / Lose

Extend game states in GameManager: add Win and Lose.

Separate panels:

UIPanelGameWin: shows Win Screen.

UIPanelGameOver: shows Lose Screen.

Update logic:

Add a parameter state in WaitBoardController (GameManager).

Add state parameter in OnConditionComplete (LevelCondition).

These decide which panel to display (Win or Lose).

Task 3: Additional Requirements

Split the two modes into separate buttons:

Add a new button in the main menu for Timer Mode.

When time runs out → trigger Game Over (instead of default Win).

Item movement animations:

Use DoTween for smooth transitions.
