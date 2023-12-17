# babyNameRank_java
PROG8580 – Computer Programming
Project 1 – Baby Names
To be completed in Groups of max 4


Assignment Requirements
•	Name your Java Class file P1<LastName><FirstInitial>etc.”. For example, A1StaceyL, for a student with the names Liz Stacey.
•	Your header comment is to include the following information:
/* Java file name
 * Purpose of program
 * 
 * Revision History:
 *     Example: Liz Stacey, 2023.03.20: Created
 */

•	Ensure you are using proper programming conventions. For example, proper variable naming, indenting, commenting, etc. Deductions will be made for each style mistake.
•	When ready, submit this completed document to the Project 1 dropbox. Pick one person to be the Project Leader. ONLY they submit files for the whole group. Your submission needs:
•	This completed document, (see below for further instructions on Team Participation portion of the document).
•	Any documents created using Visio, (can submit as an image file).
•	Original .java source file.

The Team Member Participation evaluation that is to be included as part of this document is a breakdown on the approximate percentage of work completed by each member of the group. This breakdown is agreed upon by the group and is not at the discretion of just one, or only a few, of the group members. For example, a final breakdown may look like this:
3135648 	- John Smith		30%
4567321 	- David Brown		10%
7677832 	- Mary Johnson 	60%
5456894 	- Suzan Evans		0%





Program Requirements 

The information on rankings of baby names, (male and female), in the USA between the years of 2001 and 2010 is provided to you in the zip file attached to the project. These rankings were downloaded from: www.ssa.gov/oact/babynames. Each year’s data is stored in a separate text file named babynamerankings2001.txt, babynameranking2002.txt, …, babynamerankings2010.txt. Each file contains 1000 lines. Each line contains a ranking, a boy’s name, number for the boy’s name, a girl’s name, and number for the girl’s name. For example, the first two lines in the file babynamerankings2010.txt are as follows:

1 	Jacob	21,875 	Isabella 	22,731
2 	Ethan	17,866 	Sophia 	20,477	

Based on the sample above, in 2010 the boy’s name Jacob and girl’s name Isabella were ranked #1 and the boy’s name Ethan and girl’s name Sophia were ranked #2. 21,875 boys were named Jacob and 22,731 girls were named Isabella. 

You are to write a program that loads in this data from the external text files, and then allows the user to enter a year, sex, and name to determine how popular a particular name was in a particular year.

Sample Run:

Enter the year: 2010 [Enter]
Enter the gender: M [Enter]
Enter the name: Javier [Enter]

Javier is ranked #190 in 2010
	Sample Run:

Enter the year: 2010 [Enter] 
Enter the gender: F [Enter] 
Enter the name: ABC [Enter]

The name ABC is not ranked in 2010


Hint:

Create two two-dimensional arrays to store names:

  	String[][] boyNames = new String[10][1000];
  	String[][] girlNames = new String[10][1000];

boyNames[0][0] is the name rank #1 for year 2001.
boyNames[9][10] is the name rank #11 for year 2010.
girlNames[3][8] is the name rank #9 for year 2004.
girlNames[5][342] is the name rank #343 for year 2006.



Analysis: 
Describe the problem. Answer all the following in your own words. No coding statements. 

•	State the problem to be solved.
•	List all inputs that are required and where are they coming from.
•	Discuss any restrictions to the inputs, (you are not required to code restrictions or validate inputs for this assignment).
•	List all outputs and or expected result formats. 

[insert documentation here]
We have compiled the list of all new born names (name and frequency) for a 10 year period. I am to write a code that serves as a search machine that confirms and shows the record of name and frequency when searched on it.

I have a file on my desktop named “babynames” which contains all the names and frequency at which they occur over a 10 year period (2001-2010) in a text file. Each file contains a ranked file with a boy name and its frequency it occurred  and a girl name and frequency it occur example
 1 	Jacob	21,875 	Isabella 	22,731
Which means there a 5 data to be considered (rank, boy name, frequency it occurred, girl name and its frequency) separated by space. I also imported BufferedReader and FileReader to read my file, and also IOExeption to catch any exceptions/error

After inputting the year you want to search a name, the program ask for gender of the name, if the user enters an empty string for the gender or if the input is "M," it will search for the name in the boyNames array. If the input is "F," it will search for the name in the girlNames array. If the input is an empty string or if the user is unsure, it will search both arrays and display the result if the name is found in either. 

Design: 
Create either a flowchart or pseudocode to outline all steps in solving the problem. Use Visio if you are creating a flowchart. You can export it as an image file to include it in your submission. Also, paste the image file in the space provided below.
 
 
[insert documentation and images here]

Code/Implementation: 
Create your solution using Java in a separate Java Class file. Copy and paste your code below

[insert java code here]
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

public class Main {
    public static void main(String[] args) {
        final int YEARS = 10;
        final int NAMES_PER_YEAR = 1000;

        // Two-dimensional arrays to store names
        String[][] boyNames = new String[YEARS][NAMES_PER_YEAR];
        String[][] girlNames = new String[YEARS][NAMES_PER_YEAR];

        String absolutePathPath = "/Users/HP/Downloads/BabyNamePop/baby_data";
        Path path = Paths.get(absolutePathPath);

        if (Files.isDirectory(path)) {
            System.out.println("Path is directory");
        } else {
            System.out.println("Path is not a directory");
        }
        for (int year = 0; year < YEARS; year++) {
            try {
                BufferedReader reader = new BufferedReader(new FileReader(absolutePathPath + "/babynamesranking2001.txt"));
                String line;
                int index = 0;
                while ((line = reader.readLine()) != null) {
                    //System.out.println(line);
                    String[] parts = line.split("\\s+");
                    boyNames[year][index] = parts[1];
                    girlNames[year][index] = parts[3];
                    index++;

                }

            } catch (IOException e) {
                throw new RuntimeException(e);
            }
        }

        int year, rank;
        String gender, name;
        try (BufferedReader userInput = new BufferedReader(new java.io.InputStreamReader(System.in))) {
            System.out.print("Enter the year: ");
            year = Integer.parseInt(userInput.readLine()) - 2001; // Adjust for array index

            System.out.print("Enter the gender (M/F, or leave blank if unsure): ");
            gender = userInput.readLine().toUpperCase();

            System.out.print("Enter the name: ");
            name = userInput.readLine();
        } catch (IOException | NumberFormatException e) {
            e.printStackTrace();
            return;
        }
        // Search for the name in the arrays
        if ((gender.isEmpty() || gender.equals("M")) && boyNames[year] != null) {
            rank = searchForName(boyNames[year], name);
            if (rank != -1) {
                System.out.println(name + " is ranked #" + (rank + 1) + " for boys in " + (2001 + year));
                return;
            }
        }

    }
    private static int searchForName(String[] names, String target) {
        if (names == null) {
            return -1; // Array is null, name not found
        }
        for (int i = 0; i < names.length; i++) {
            if (names[i] != null && names[i].equalsIgnoreCase(target)) {
                return i;
            }
        }
        return -1; // Name not found
    }
}



 

Testing: 
Describe your testing process. 

•	What test cases did you use, and how were the results verified? 
•	What errors did you come across and what did you do to fix them? 

Include screenshots of your tests you ran to verify your results. Screenshots must show both code and output.


 
[insert documentation and images here]

Task List:  
List which team member completed which task.

[insert documentation here]

Team Member Participation: 
Team member participation evaluation that is agreed by the group. This is a percentage breakdown of how much work was done by each student.

[insert documentation here]
