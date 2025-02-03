## Turtles Arduino Code Generation

>To work around an annoying and long-standing GitHub Classroom bug and get the autograder to work reliably, you will have to undertake a couple of extra steps:
>
>1. Open [classroom.yml](.github/workflows/classroom.yml) and click on the little pencil symbol to edit the file.
>2. Add a space somewhere and remove it again (yes, that means the file content won't have changed), then click on the "Commit..." button that has now become enabled. Accept the standard choices and commit. This should allow the auto-grader to run in the future.

Create a code generator to generate Arduino code for a simple [turtle robot](https://github.com/jringert/gendev.bot/tree/main/gendev.bot.esp8266). The starting point is the file `/uk.ac.kcl.inf.mdd4.turtles/src/uk/ac/kcl/inf/mdd4/generator/TurtlesGenerator.xtend`.

This file already contains a head and tail of the program. You will focus on translating the `TurtleProgram` to the inner loop of the generated Arduino code.

1. The generated file must have extension `ino` and be in a folder of the same name as the file, e.g., turtle program `move.turtles` should be generated with in folder `move.turtles` with filename `move.turtles.ino`.

2. Follow the instructions on the slides on how to translate move and turn statements.
    - Remember that sometimes return types, e.g., `String` must be declared for `dispatch` methods.

3. Implement loops as `for`-loops with integer `int i=0` (name clashes when nesting are no problem) and generate nothing for variables (see why below). 

4. To save computation resources on the Arduino, evaluate all `IntExpressions` directly to integers in Xtend (also resolve values of variables directly).
    - Our `Addition` and `Multiplication` are not trivial and you might want to write a separate method to handle them. 
    - When working with lists the methods `.head` for the first element and `.tail` for all other elements might be helpful.

5. To save space on the Arduino, combine all consecutive `MoveStatements` to a single one where you add or substract the steps based on the current command.
    - One way is to go over the list of statements and combine them into a new list where the next statement is combined with the `.tail` of the new list, if possible.
    - Remember that loops also have nested lists of statements that you want to combine inside the loop.
    - To add or substract steps you need to create a new `Addition` object via the generated factory `TurtlesFactory`, e.g., `var add = TurtlesFactory.eINSTANCE.createAddition()`.

For all steps you may look for inspiration in the previous code generator we developed.

Eventually, the autograding should pass and assign 30/30.

### Using the repository

There are two ways to do this activity:

1. You can check out the repository and import the projects into Eclipse, then do the activity there. Commit your changes and push them back to GitHub to trigger the autograding so you can see whether you've correctly implemented the grammar. More information about checking out and editing code in Eclipse can be found on KEATS.
2. You can do this activity in your browser.

   Due to an annoying, long-standing GitHub Classroom bug, you need a small extra step for this:

    1. Copy the URL of your repository (see the location bar of your browser).
    2. Open [this form](https://7ccsmmdd.github.io/) and paste your repository URL into the corresponding field.
    3. The URL field should fill with a long complicated URL as soon as you move out of the text field. 
    4. Click on the button at the bottom of the form to open that URL in a new tab: this is the MDENet Education Platform with the activity pre-loaded. You can view visualisations of the meta-model, edit your grammar and test out the changes you have made by generating an editor. See the video on KEATS to find out how to do this. **Note that you must save your changes before switching to the generated editor or you will lose them.** Saving your changes will create a commit in your repository, which will also automatically trigger the autograding process.
