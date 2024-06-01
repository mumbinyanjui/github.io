# sudoku copy and add project
This was an excercise that i was going through in python.
It was all about sudoku board game.where there is a pre-defined board.
On having the board i was supposed to create a function that copies the  original sudoku and alters the given index of the copied sudoku.
Below is the specific instructions in order to complete the task

The function copy_and_add(sudoku: list, row_no: int, column_no: int, number: int) takes a two-dimensional array representing a sudoku grid, two integers referring to the row and column indexes of a single square, and a single digit between 1 and 9, as its arguments. 
The function should return a copy of the original grid with the new digit added in the correct location. 
The function should not change the original grid received as a parameter.

The print_sudoku function from the previous exercise could be useful for testing, and it is used in the example below:
## for the print_sudoku function it was the previous exercise which also was a function taking a two dimensional list as its argument and then printing the sudoku grid with the zeros replaced with dashes and printing the number if any.
## Below is the function for the print_sudoku
```.py
def print_sudoku(sudoku):
    for row in sudoku:
        for square in row:
            if square > 0:
                print(f" {square}", end="")
            else:
                print(" _", end="")
            
        print()
```
This made me scratch my head thinking on how to solve the exercise.
As any person would think without complicating things i thought of just coping the original sudoku to a new one using the ## [:] operator.
### here's the function
```.py
def copy_and_add(sudoku: list, row : int , column : int , number : int):
    new_sudoku=sudoku[:]
    new_sudoku[row][column] = number
    return new_sudoku
```
The above function was archiving the goal of copying but on calling the copy_and_add function the original sudoku was being altered.
So I had to look for an alternative solution which would help me archive my goal.
Its when i thought of using a handy code to see if i can archive something, by handy code i mean, since i already know the number of rows that needed to be copied, then i can copy each row separately using the copy() function and append the rows to the new_sudoku[].
### here's the code
```.py
def copy_and_add(sudoku: list, row : int , column : int , number : int): 
    row1 = sudoku[0].copy()
    row2 =sudoku[1].copy()
    row3 = sudoku[2].copy()
    row4 =sudoku[3].copy()
    row5 = sudoku[4].copy()
    row6 =sudoku[5].copy()
    row7 = sudoku[6].copy()
    row8 =sudoku[7].copy()
    row9 = sudoku[8].copy()
    new_sudoku = [row1,row2,row3,row4,row5,row6,row7,row8,row9]
    new_sudoku[row][column] = number
    return new_sudoku
```
After testing the code i was like "HURRAY I DID IT!!" but that was not it coz the next question was *what if the number of rows are not known?
So i had to look for a solution that actually solved the problem without having other questions and problems arising.This gave me the idea of using the nested for loop.
where i declared an empty list new_sudoku[] and iterated through the rows first then below it declared another empty list rows[] which was to store all the elements in each row in separate list.
Below it i used another for loop to iterate through the columns in each row and then append each item in every row in the list rows[],after a row has been appended successfully ,append the rows [] to the new sudoku [].
### here's the code
```.p
def copy_and_add(sudoku: list, row : int , column : int , number : int):
    new_sudoku=[]
    print(my_sudoku)
    for i in sudoku:
        rows =[]
        for j in i:
              rows.append(j)
        new_sudoku.append(rows)            
    new_sudoku[row][column] = number
    return new_sudoku
```
### below is the final code to achive copying a new sudoku and appending a number on the specified index using the row and column
```.py
def copy_and_add(sudoku: list, row : int , column : int , number : int):
    new_sudoku=[]
    print(my_sudoku)
    for i in sudoku:
        rows =[]
        for j in i:
              rows.append(j)
        new_sudoku.append(rows)            
    new_sudoku[row][column] = number
    return new_sudoku

def print_sudoku(sudoku):
    for row in sudoku:
        for square in row:
            if square > 0:
                print(f" {square}", end="")
            else:
                print(" _", end="")
            
        print()

        # Write your solution here

if __name__ =="__main__":
    
    grid_copy= copy_and_add(my_sudoku,0,0,2)
    print("original")
    print_sudoku(my_sudoku)
    
    print()
    print("copy")
    print_sudoku(grid_copy)
```
