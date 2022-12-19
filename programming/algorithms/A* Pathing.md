c.f. http://theory.stanford.edu/~amitp/GameProgramming/ImplementationNotes.html

A specialization of [[Dijkstra's algorithm]], often used for finding the shorted path between two node in a 2D grid.

Essentially a [[Breadth-first search]], where the next node to be processed is selected according to a heuristic weight.  The weight consists of two factors:
1. The movement cost `M score` *from* the starting point *to* the candidate position.
2. The estimated movement cost `H score` *from* the candidate position *to* the destination.  Unless distances have been pre-calculated, this is necessarily an estimate/heuristic, since we haven't chosen a path yet.
3. The final heuristic weight of a candidate (`total score`) is `M score` + `H score`.

## Description
Setup 2 data structures: 1 to keep nodes waiting to be processed (`open` store), and 1 to track nodes that have already been processed (`closed` store).  `open` is initally populated with the starting node.  At each iteration we remove the node from `open` that has the smallest `total score` and add it to `closed`.  We then calculate a `total score` for each eligible neighbor.  If a neighbor is the destination, we're done.  Otherwise, if `closed` already contains the neighbor cell, check the `f` value of the closed cell.  If it is **greater** than the value of the current neighbor, i.e. the `close`d cell is a lower priority than the neighbor currently being considered, remove the coordinate from `closed` and go to the next steps.  Otherwise, the current iteration is done.  Finally, check for the neighbor cell in `open`.  If it exists **and** the cell in `open` is a lower priority than the neighbor under consideration, replace the cell in `open` with the neighbor.  If the neighbor does not exist in either store, add it to `open`.

## Calculating `H score`
c.f. 
Different strategies are appropriate for different situations.  The simplest, appropriate for a 2D plane with 2 movement axes, is to take the absolute value of the difference between the destination `x` and the candidate `x`, and add that number to the absolute value of the difference between the destination `y` and the candidate `y`.  So,
```Math
Hscore = (
Math.abs(destination.x - candidate.x) +
Math.abs(destination.y - candidate.y)
)
```

## Tracing the path
As we process nodes, add to each processed node a reference to their parent.  When we find the destination node, return it.  We can then trace the references backwards from the destination to the source node.