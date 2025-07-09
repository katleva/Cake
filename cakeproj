'use strict';
const prompt = require('prompt-sync')();
const cakeRecipes = require(`./cake-recipes.json`);
const savedRecipes = []


function getAuthors(recipes) {
  const authors = [];
  recipes.forEach(recipe => {
    if (!authors.includes(recipe.Author)) {
      authors.push(recipe.Author)
    }
  });
  return authors.sort();
}


function getRecipeNames(recipes) {
    if (!recipes) {
  console.log("No recipes found.")
  return; 
}

for (const { Name } of recipes) {
    console.log(Name)
  }
}


function getRecipesByAuthor(recipes, author) {
  return recipes.filter(recipe => recipe.Author.toLowerCase().includes(author.toLowerCase())
)
}


function givenIngredient(recipes, ingredient) {
  return recipes.filter(recipe => recipe.Ingredients.some(getRecipeNames => getRecipeNames.toLowerCase().includes(ingredient.toLowerCase()))
)
}


function recipeNameMatch(recipes, names) {
const recipeFound = recipes.find(recipe => 
  recipe.Name.toLowerCase().includes(names.toLowerCase()))
  if (!recipeFound) {
    return null
  } 

  return recipeFound;
}


function getAllIngredients(recipes) {
  return recipes.reduce((allIngredients, recipe) => {
    return [...allIngredients, ...recipe.Ingredients];
  }, []);
}


const displayMenu = () => {
  console.log("\nRecipe Management System Menu:");
  console.log("1. Show All Authors");
  console.log("2. Show Recipe names by Author");
  console.log("3. Show Recipe names by Ingredient");
  console.log("4. Get Recipe by Name");
  console.log("5. Get All Ingredients of Saved Recipes");
  console.log("0. Exit");
  const choice = prompt("Enter a number (1-5) or 0 to exit: ");
  return parseInt(choice);
}


let choice;

do {
  choice = displayMenu();

  switch (choice) {
    case 1:
      const authors = getAuthors(cakeRecipes);
      console.log(authors);
       break;

    case 2:
     const whichAuthor = prompt("SEARCH FOR AN AUTHOR: ");
     const foundAuthor = getRecipesByAuthor(cakeRecipes, whichAuthor);

     if (foundAuthor.length === 0) {
      console.log("No results for author. ")
     } else {
     getRecipeNames(foundAuthor);
     }
       break;

    case 3:
      const whichIngredient = prompt("SEARCH FOR INGREDIENT:  ")
      const foundIngredient = givenIngredient(cakeRecipes, whichIngredient);
      foundIngredient.forEach(({ Name }) => console.log(Name));
       break;

    case 4:
      const whichRecipeName = prompt("SEARCH RECIPE BY NAME: ")
      const foundRecipe = recipeNameMatch(cakeRecipes, whichRecipeName);

       if (foundRecipe) {
         console.log("Name: ", foundRecipe.Name)
         console.log("Link: ", foundRecipe.url)
         console.log("Description: ", foundRecipe.Description)
         console.log("Author: ", foundRecipe.Author)
         console.log("Ingredients: ", foundRecipe.Ingredients)
         console.log("How to cook: ", foundRecipe.Method)

         const save = prompt("Would you like to save this recipe? (yes/no): ").toLowerCase();
        if (save === 'yes' || save === 'y') {
         savedRecipes.push(foundRecipe);
         console.log("Recipe saved. ");
        } else {
         console.log("Recipe not saved. ");
    }
       } else {
        console.log("Recipe not found. ")
       }
  
        break;

    case 5:
      const savedRecipesIngredients = getAllIngredients(savedRecipes)
       if (savedRecipes.length === 0) {
  console.log("No saved recipes yet.");
       } else {
        savedRecipes.forEach(recipe => {
    console.log(`\nIngredients for: ${recipe.Name}`);
    recipe.Ingredients.forEach((ingredient, index) => {
    console.log(`${index + 1}. ${ingredient}`);
    });
  });
}

       break;
    case 0:
      console.log("Exiting...");
      break;
    default:
      console.log("Invalid input. Please enter a number between 0 and 5.");
  }
} while (choice !== 0);

// either Dutch or English is okay
