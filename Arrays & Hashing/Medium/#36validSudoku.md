# 36. Valid Sudoku

Determine if a `9x9` Sudoku board is valid. Only the filled cells need to be validated according to the following rules:
1. Each row much contain the digits `1-9` without repetition
2. Each column must contain the digits `1-9` without repetition
3. Each of the nine `3x3` sub-boxes of the grid must contain the digits `1-9` without repeition

- notes: there are going to be empty positions and for the sake of this problem, a sudoku that has a row filled from 1-8 and the last box is empty and a column using that same empty box filled from 2-9 would still be a valid solution. The empty box needs to be filled with a 9 or a 1, but for this problem it doesn't matter.

- solution: use a hashset for rows, columns, and the 3x3 sub-box
    - as for the 3x3 sub-box, we can picture grouping up the indices as one index. For example: indices 0, 1, and 2 for both the rows and columns are part of the first 3x3 sub-box. We can group 0, 1, and 2 to be index 1 by dividing each real index by 3 and flooring it (0 // 3 = 0, 1 // 3 = 0, 2 // 3 = 0)
    - check for duplicates: if there is one, then return false and if there are no duplicates then return true

```python
def isValidSudoku(self, board: List[List[str]]) -> bool:
    # create a set for each "check" for the sudoku board
    cols = defaultdict(set)
    rows = defaultdict(set)
    squares = defaultdict(set)

    # iterates through each row and column
    for r in range(9):
        for c in range(9):
            # skips if there is a dot
            if board[r][c] == ".":
                continue
            # checks if the current number is already in the corresponding row set, column set, or square set
            if (board[r][c] in rows[r] or board[r][c] in cols[c] or board[r][c] in squares[(r // 3, c // 3)]):
                return False
            cols[c].add(board[r][c])
            rows[r].add(board[r][c])
            squares[(r // 3, c // 3)].add(board[r][c])
    return True
```
- Time: `O(1)`
- Space: `O(1)`

## Example

1. `Input: board = `
[["5","3",".","5","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
2. `r = 0`, `c = 0`
3. `board[0][0] = 5`
4. `rows[0]`, `cols[0]`, `squares[(0 // 3, 0 // 3)] = squares[(0, 0)]` None of them contain 5
5. `rows[0] = {'5'}`, `cols[0] = {'5'}`, `squares[(0, 0)] = {'5'}`
6. Insert 3 into `rows[0]`, `cols[1]`, `squares[(0, 0)]`
7. Skip the `.`
8. `rows[0]` has a `5` already in the set, so
9. return `False`