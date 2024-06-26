  
**Link:** https://leetcode.com/problems/snakes-and-ladders/  
#### Solution:  
  
**Topics**: [BFS](../DSA/BFS.md), [set](set.md)  
  
**Intuition**  
Classic shortest path problem BFS problem with some edge cases in the way it's set up. Because the positions are 1 indexed, its way more convenient to flatten the board into a 1d array and use the snake/ladders to index directly into the respective position.  
  
Once that's done, we simply perform a BFS starting a position 1 (or 0 if 0-indexed). We add to the queue the first 6 positions in front of the current position. If one of those positions is either a snake or a ladder, we add the value to the queue.  
  
Keep a visited set on the positions to prevent cycles. For some reason that I can't understand, modifying the board in-place for cycle prevention fails some test cases...just keep it simple and use a set.  
  
**Implementation**  
```python  
def snakes_and_ladders(board):  
	flat = []  
	flip = False  
	for row in board[::-1]:  
		row = row[::-1] if flip else row  
		flat += row  
		flip = not flip  
  
	visited = set()  
	queue = deque([(0, 0)])  
	while queue:  
		pos, moves = queue.popleft()  
		if pos in visited:  
			continue  
		if pos == len(flat)-1:  
			return moves  
  
		visited.add(pos)  
		for new_pos in range(pos+1, min(pos+7, len(flat))):  
			if flat[new_pos] == -1:  
				queue.append((new_pos, moves+1))  
			else:  
				queue.append((flat[new_pos]-1, moves+1))  
	return -1  
  
#time: o(n**2)  
#memory: o(n**2)  
```  
  
**Visual**   
![IMG_CD4B68DCA468-1.jpeg](./_pics/IMG_CD4B68DCA468-1.jpeg)  
  
  
#review   
#hard   
  
  
