# Twisty Little Maze
A simple Playdate game that demonstrates restricting the player's movement to the horizontal or vertical axis in the Pulp tile-based game engine.

![](twisty-little-maze-demo.gif)

The approach used here has four parts:

 1. We store the "real" player location in two globals, `player_x` and `player_y`
 2. We only update `player_x` when motion is allowed in the horizontal direction, and only update `player_y` when motion is allowed in the vertical direction.
 3. Because the Pulp framework will automatically update the player's position, we have to immediately correct it back to `player_x`, `player_y` using `goto`.
 4. Because an `update` even will be generated following the `goto`, we also have to suppress the update handler in that case. To do this, we set another global, `goto_triggered`, before executing the `goto`, and then, in the handler, when `goto_triggered` is set, we do nothing except clear `goto_triggered`.

None of the built-in solid object collision detection works when we do the above, so we also have to add our own checks for what the player is allowed to pass through. As you'll see in the game (and code!), this also opened the door *ahem* for some additional features.
