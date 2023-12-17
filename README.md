# babyNameRank_java

#  Baby Name Ranking Java Program

![](10.jpg) 

**Technology used**

- Intellij
- Draw.io

**Analysis**:

Describe the problem. Answer all the following in your own words. No coding statements. 

•	State the problem to be solved.
•	List all inputs that are required and where are they coming from.
•	Discuss any restrictions to the inputs, (you are not required to code restrictions or validate inputs for this assignment).
•	List all outputs and or expected result formats. 

**Problem**

We have compiled the list of all new born names (name and frequency) for a 10 year period. I am to write a code that serves as a search machine that confirms and shows the record of name and frequency when searched on it.

I have a file on my desktop named “babynames” which contains all the names and frequency at which they occur over a 10 year period (2001-2010) in a text file. Each file contains a ranked file with a boy name and its frequency it occurred  and a girl name and frequency it occur example

 1 	Jacob	21,875 	Isabella 	22,731

Which means there a 5 data to be considered (rank, boy name, frequency it occurred, girl name and its frequency) separated by space. I also imported BufferedReader and FileReader to read my file, and also IOExeption to catch any exceptions/error

After inputting the year you want to search a name, the program ask for gender of the name, if the user enters an empty string for the gender or if the input is "M," it will search for the name in the boyNames array. If the input is "F," it will search for the name in the girlNames array. If the input is an empty string or if the user is unsure, it will search both arrays and display the result if the name is found in either. 

**Design**:

Create either a flowchart or pseudocode to outline all steps in solving the problem. Use Visio if you are creating a flowchart. You can export it as an image file to include it in your submission. Also, paste the image file in the space provided below.
 
![](001.png) 

**Code/Implementation**:

		import java.io.*;
		import java.nio.file.Files;
		import java.nio.file.Path;
		import java.nio.file.Paths;

		public class Main {
    		public static void main(String[] args) {
        		// Constants for years and names per year
        		final int YEARS = 10;
        		final int NAMES_PER_YEAR = 1000;

        		// Two-dimensional arrays to store names
        		String[][] boyNames = new String[YEARS][NAMES_PER_YEAR];
        		String[][] girlNames = new String[YEARS][NAMES_PER_YEAR];

        		// Path to the directory containing baby name data files
        		String absolutePathPath = "/Users/HP/Downloads/BabyNamePop/baby_data";
        		Path path = Paths.get(absolutePathPath);

        		// Check if the provided path is a directory
        		if (Files.isDirectory(path)) {
            		System.out.println("Path is a directory");
        		} else {
            		System.out.println("Path is not a directory");
        		}

        		// Populate the arrays with baby names data from text files
        		for (int year = 0; year < YEARS; year++) {
            		try {
                		// Read data from the baby names ranking file for a specific year
                		BufferedReader reader = new BufferedReader(new FileReader(absolutePathPath + "/babynamesranking" + (2001 + year) + ".txt"));
                		String line;
                		int index = 0;
                		while ((line = reader.readLine()) != null) {
                    		String[] parts = line.split("\\s+");
                    		boyNames[year][index] = parts[1];
                    		girlNames[year][index] = parts[3];
                    		index++;
                		}
            		} catch (IOException e) {
                		throw new RuntimeException(e);
            		}
        		}

        		// User input for the name search
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

    		// Method to search for a name in an array
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
 

**Testing**: 

Describe your testing process. 

•	What test cases did you use, and how were the results verified? 
•	What errors did you come across and what did you do to fix them? 

Include screenshots of your tests you ran to verify your results. Screenshots must show both code and output.




