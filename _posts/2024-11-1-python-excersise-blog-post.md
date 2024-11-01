# Below is a python excersise that I took and found to be very helpful , very detailed and very involving.
# The excersise reqires the following:
   ### 1.Create a Recipe Class and a RecipeBook Class.
   ### 2.Write methods for the RecipeBook Class:
            a).add_recipe method. 
            b).remove_recipe method.
            c).recipe_by_name method.
            d).recipes_containing_ingredients method.
            e).recipes_within_time method that takes an integer as an argument.
            f).recipes_with_all_ingredients method.
            g).all_recipes method.
  ### 3.Write an interactive user interface. 
  ### 4.Ensure there's a persistent storage for a recipe management program.
## 1.Create a Recipe Class and a RecipeBook Class.
a).Recipe class.
In this  class we define and declare the variables that will be used in this whole program.
```.py
class Recipe:
    def __init__(self, name: str, ingredients: list, time: int, instructions: str):
        self.name = name
        self.ingredients = ingredients
        self.time = time
        self.instructions = instructions

    def __repr__(self):
        return f"Recipe(name='{self.name}', ingredients={self.ingredients}, time={self.time}, instructions='{self.instructions}')"
```
b).RecipeBook Class.
  ## 2.Write methods for the RecipeBook Class:
In this class we define the methods that will be used in the program.
##### a).add_recipe method. 
The method adds the given Recipe object to the __recipe_book attribute. You can assume that no two recipes with the same name will be added.
##### b).remove_recipe method. 
The method removes the given Recipe object from the __recipe_book attribute. You can assume that only existing Recipe objects are attempted to be removed.
##### c).recipe_by_name method. 
The method takes a string as an argument. The method returns a Recipe object whose name matches the given string. If no matching recipe object is found, the method should return None.
##### d).recipes_containing_ingredients method. 
The method takes a list of strings as an argument. The method returns a list of Recipe objects, each of which contains all of the specified ingredients in its attributes. If no Recipe objects matching the criteria are found, the method should return an empty list.
##### e).recipes_within_time method that takes an integer as an argument. 
The method returns a list of Recipe objects whose cooking time is at most equal to the given argument. If no recipe objects matching the criteria are found, the method should return an empty list.
##### f).recipes_with_all_ingredients method. 
The method takes a list of strings as an argument. The method returns a list of all Recipe objects whose ingredients are all found in the list given to the method. If no recipe objects matching the criteria are found, the method should return an empty list.
##### g).all_recipes method.      
The method returns a list containing all the Recipe objects stored in the RecipeBook object. If the list returned by the method is modified, it does not affect the RecipeBook object.

```.py
class RecipeBook:
    def __init__(self):
        self.__recipe_book = []
        self.load_recipes()
        self.initialize_default_recipes()

    def add_recipe(self, recipe: Recipe):
        self.__recipe_book.append(recipe)
        self.save_recipes()

    def remove_recipe(self, recipe: Recipe):
        self.__recipe_book.remove(recipe)
        self.save_recipes()

    def recipe_by_name(self, name: str):
        for recipe in self.__recipe_book:
            if recipe.name == name:
                return recipe
        return None

    def recipes_within_time(self, max_time: int):
        return [recipe for recipe in self.__recipe_book if recipe.time <= max_time]

    def all_recipes(self):
        return self.__recipe_book.copy()

    def clear_memory(self):
        self.__recipe_book.clear()
        self.save_recipes()

    def save_recipes(self):
        with open("recipes.txt", "w") as file:
            for recipe in self.__recipe_book:
                ingredients_str = ",".join(recipe.ingredients)
                file.write(f"{recipe.name};{ingredients_str};{recipe.time};{recipe.instructions}\n")

    def load_recipes(self):
        if os.path.exists("recipes.txt"):
            with open("recipes.txt", "r") as file:
                for line in file:
                    name, ingredients_str, time_str, instructions = line.strip().split(";")
                    ingredients = ingredients_str.split(",")
                    time = int(time_str)
                    recipe = Recipe(name, ingredients, time, instructions)
                    self.__recipe_book.append(recipe)

    def initialize_default_recipes(self):
        default_recipes = [
            Recipe("Chicken", ["Chicken", "Salt"], 15, "Fry the chicken. Add salt."),
            Recipe("Caesar Salad", ["Lettuce", "Chicken", "Dressing"], 25, "Cook the chicken. Place lettuce on a plate. Add chicken. Add dressing."),
            Recipe("Blueberry Muffins", ["Flour", "Milk", "Sugar", "Blueberries"], 30, "Mix ingredients. Bake muffins at 180 degrees."),
        ]
        for recipe in default_recipes:
            if not self.recipe_by_name(recipe.name):  # Check if it already exists
                self.add_recipe(recipe)
```
There are some additional programs that are found in the RecipeBook,these are:
##### h).clear_memory.
This method is used to clear the memory of the RecipeBook by clearing all the recipe in it.
##### i).save_recipes.
This method is used to save or write the recipes in the RecipeBook in a file formart.Which has the following instructions to be followed:
##### The properties of the storage are the following:
##### <i>i.Implement the storage in file named "recipes.txt"</i>
##### <i>ii.If the file does not exist, the program will create it.</i>
##### <i>iii.The program saves the data to the file every time a recipe is added or removed.</i>
##### <i>iv.The storage format in the file should be as follows: **`<recipe name>;<ingredient1>,<ingredient2>,<etc>;<cooking time>;<instructions>`**</i>

##### j).load_recipes.
<i>In this method we have to import os in order to be able to load our file.Which is done as the first thing in the program
```.py
import os # This is to be written as the first line of code just incase yoou have errors running the code above
```
This method is used to load or read the context(ie.all the recipes ) of the file created.
##### k).initialize_default_recipes.
This method is used to initialize some few recipes in our RecipeBook.

## 3.Write an interactive user interface. 
This is done under a function named main
##### The user interface should have the following functionality:

When the program starts, it should print "Recipe book program" and instructions for the user interface. See the example below.
##### The program asks the user to make a selection.
##### i).Selection 0: 
**`Exit.`** End the program execution.
##### ii).Selection 1: 
**`Add recipe.`** The program asks the user for the recipe name, cooking time, ingredients, and instructions, and saves the information. If a recipe with the same name already exists, the program will not ask for additional information and the recipe is not saved. The program prints the information to the user as shown in the example below.
##### iii).Selection 2: 
**`Remove recipe.`** The program asks the user for the name of the recipe and based on that, it deletes the recipe if it exists. The program prints the information about the event to the user. If the recipe to be deleted is found, the program prints "Removed recipe <recipe_name>". Otherwise, the program prints "No recipe found with name <recipe_name>".
##### iv).Selection 3: 
**`Search recipe by name.`** The program asks the user for a name of a recipe and prints the recipe if found. If the recipe is not found, the program prints "No recipe found with name <searched_name>". Otherwise, the program prints the details of the recipe according to the example below:
##### v).Selection 4:
**`Search recipe by preparation time.`** The program asks the user for an integer, which is the maximum acceptable cooking time for a recipe. The program prints a list containing all the recipes with a cooking time equal to or less than the given time.
##### vi).Selection 5: 
**`Return all recipes.`** The program prints all the recipes as shown in the example below. If no recipes are found, the program prints "No recipes found".
##### vii).Selection 6: 
**`Clear memory.`** The program removes all known recipes, including the recipes saved in the file.
##### For any other input, the program prints the instructions again.

```.py
def main():
    recipe_book = RecipeBook()
    
    print("Recipe book program")
    print("Commands:")
    print("0 - Exit")
    print("1 - Add recipe")
    print("2 - Remove recipe")
    print("3 - Search recipe by name")
    print("4 - Search recipe by preparation time")
    print("5 - Return all recipes")
    print("6 - Clear memory")
    
    while True:
        command = input("Enter command: ")
        
        if command == '0':
            break
        elif command == '1':
            name = input("Enter recipe name: ")
            if recipe_book.recipe_by_name(name):
                print("Recipe already exists")
                continue
            
            ingredients = input("Enter recipe ingredients separated by comma: ").split(",")
            cooktime = int(input("Enter recipe cooktime (min): "))
            instructions = input("Enter recipe instructions: ")
            recipe = Recipe(name, ingredients, cooktime, instructions)
            recipe_book.add_recipe(recipe)
            print(f"Added recipe {name}")
        
        elif command == '2':
            name = input("Enter name of recipe to remove: ")
            recipe = recipe_book.recipe_by_name(name)
            if recipe:
                recipe_book.remove_recipe(recipe)
                print(f"Removed recipe {name}")
            else:
                print(f"No recipe found with name {name}")
        
        elif command == '3':
            name = input("Enter recipe name to search: ")
            recipe = recipe_book.recipe_by_name(name)
            if recipe:
                print("Found recipe:")
                print(recipe)
            else:
                print(f"No recipe found with name {name}")
        
        elif command == '4':
            max_time = int(input("Enter the preparation time of the recipe you're looking for (min): "))
            found_recipes = recipe_book.recipes_within_time(max_time)
            if found_recipes:
                print(f"Found recipes with preparation time {max_time} min:")
                for r in found_recipes:
                    print(r)
            else:
                print(f"No recipes found with preparation time {max_time} min.")
        
        elif command == '5':
            all_recipes = recipe_book.all_recipes()
            if all_recipes:
                print("Found recipes:")
                for r in all_recipes:
                    print(r)
            else:
                print("No recipes found.")
        
        elif command == '6':
            recipe_book.clear_memory()
            print("Memory cleared")
        
        else:
            print("Commands:")
            print("0 - Exit")
            print("1 - Add recipe")
            print("2 - Remove recipe")
            print("3 - Search recipe by name")
            print("4 - Search recipe by preparation time")
            print("5 - Return all recipes")
            print("6 - Clear memory")
```
### Finally you have to run the main function using **`if__name__=="__main__:`**
```.py
if __name__ == "__main__":
    main()
```
### Example of how the user interface works when adding and removing recipes:
```.py
Recipe book program
Commands:
0 - Exit
1 - Add recipe
2 - Remove recipe
3 - Search recipe by name
4 - Search recipe by preparation time
5 - Return all recipes
6 - Clear memory
Enter command: 1
Enter recipe name: Chicken
Enter recipe ingredients separated by comma: Chicken,Salt
Enter recipe cooktime (min): 15
Enter recipe instructions: Fry the chicken. Add salt.
Added recipe Chicken
Enter command: 1
Enter recipe name: Fish
Enter recipe ingredients separated by comma: Fish,Salt,Dill
Enter recipe cooktime (min): 35
Enter recipe instructions: Add salt and dill to the fish. Fry the fish.
Added recipe Fish
Enter command: 1
Enter recipe name: Chicken
Recipe already exists
Enter command: 2
Enter name of recipe to remove: Fish
Removed recipe Fish
Enter command: 2
Enter name of recipe to remove: Fish
No recipe found with name Fish
Enter command: 1
Enter recipe name: Blueberry muffins
Enter recipe ingredients separated by comma: Flour,Milk,Sugar,Blueberries
Enter recipe cooktime (min): 30
Enter recipe instructions: Mix the ingredients. Bake at 180 degrees.
Added recipe Blueberry muffins
Enter command: 5
Found recipes:
Recipe(name='Chicken', ingredients=['Chicken', 'Salt'], time=15, instructions='Fry the chicken. Add salt.')
Recipe(name='Blueberry muffins', ingredients=['Flour', 'Milk', 'Sugar', 'Blueberries'], time=30, instructions='Mix the ingredients. Bake at 180 degrees.')
Enter command: 0
```
### Example of recipe search when the program starts with chicken, fish, and blueberry muffin recipes already in memory:
```.py
Recipe book program
Commands:
0 - Exit
1 - Add recipe
2 - Remove recipe
3 - Search recipe by name
4 - Search recipe by preparation time
5 - Return all recipes
6 - Clear memory
Enter command: 3
Enter recipe name to search: Pizza
No recipe found with name Pizza
Enter command: 3
Enter recipe name to search: Blueberry muffins
Found recipe:
Recipe(name='Blueberry muffins', ingredients=['Flour', 'Milk', 'Sugar', 'Blueberries'], time=30, instructions='Mix the ingredients. Bake at 180 degrees.')
Enter command: 4
Enter the preparation time of the recipe you're looking for (min): 25
Found recipes with preparation time 25 min:
Recipe(name='Chicken', ingredients=['Chicken', 'Salt'], time=15, instructions='Fry the chicken. Add salt.')
Enter command: 5
Found recipes:
Recipe(name='Chicken', ingredients=['Chicken', 'Salt'], time=15, instructions='Fry the chicken. Add salt.')
Recipe(name='Fish', ingredients=['Fish', 'Salt', 'Dill'], time=35, instructions='Add salt and dill to the fish. Fry the fish.')
Recipe(name='Blueberry muffins', ingredients=['Flour', 'Milk', 'Sugar', 'Blueberries'], time=30, instructions='Mix the ingredients. Bake at 180 degrees.')
Enter command: 0
```
### Finally, an example of how the program handles undefined commands and clears memory when recipes exist when starting the program:
```.py
Recipe book program
Commands:
0 - Exit
1 - Add recipe
2 - Remove recipe
3 - Search recipe by name
4 - Search recipe by preparation time
5 - Return all recipes
6 - Clear memory
Enter command: 5
Found recipes:
Recipe(name='Chicken', ingredients=['Chicken', 'Salt'], time=15, instructions='Fry the chicken. Add salt.')
Recipe(name='Fish', ingredients=['Fish', 'Salt', 'Dill'], time=35, instructions='Add salt and dill to the fish. Fry the fish.')
Recipe(name='Blueberry muffins', ingredients=['Flour', 'Milk', 'Sugar', 'Blueberries'], time=30, instructions='Mix the ingredients. Bake at 180 degrees.')
Enter command: 6
Memory cleared
Enter command: 5
No recipes found
Enter command: 6
Memory cleared
Enter command: X
Commands:
0 - Exit
1 - Add recipe
2 - Remove recipe
3 - Search recipe by name
4 - Search recipe by preparation time
5 - Return all recipes
6 - Clear memory
Enter command: 11
Commands:
0 - Exit
1 - Add recipe
2 - Remove recipe
3 - Search recipe by name
4 - Search recipe by preparation time
5 - Return all recipes
6 - Clear memory
Enter command: 0
```
  
