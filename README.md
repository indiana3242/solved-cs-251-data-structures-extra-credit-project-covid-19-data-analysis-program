Download Link: https://assignmentchef.com/product/solved-cs-251-data-structures-extra-credit-project-covid-19-data-analysis-program
<br>
<h2>Assignment</h2>

The assignment is to use a C++ <strong>map</strong> data structure (and other data structures if needed) to input and analyze daily reports surrounding the Covid-19 virus.  Since this is an extra credit project, it’s an all-or-nothing proposition:  you must score 100 via the autograder, you must meet all requirements, no partial credit, etc.  This is not meant to be a hard project, in fact it’s a good project that puts into practice all the things we’ve been working on:  data structures, functional design, encapsulation, file input.  But we don’t have a lot of resources to devote to grading, so be sure to follow the project and autograding requirements.  Here’s the main screen for the program:










In short, the program supports 6 commands:




<ol>

 <li><strong>help</strong></li>

 <li>Lookup and display of data by country <strong>&lt;name&gt;</strong></li>

 <li>List all <strong>countries</strong> in alphabetical order with data from most recent daily report</li>

 <li>List the <strong>top10</strong> countries based on # of confirmed cases</li>

 <li>List the world-wide <strong>totals</strong> (confirmed, deaths, recovered)</li>

 <li>A command of your own choice</li>

</ol>




We would encourage folks to post what they are doing for #6 on Piazza, to generate more ideas.  Lots and lots of possibilities.

<h2>Programming Environment</h2>

You are free to program on whatever platform you want, using whatever C++ compiler / programming environment you want.  We are providing a Codio project <strong>cs251-extra-credit—covid-19</strong> containing the input files and a starter “main.cpp” file; these are also provided on the course <a href="https://www.dropbox.com/sh/49apjz0efhdnukp/AADszPAg3-Ag1CM6suYGuzP9a?dl=0">dropbox</a><a href="https://www.dropbox.com/sh/49apjz0efhdnukp/AADszPAg3-Ag1CM6suYGuzP9a?dl=0">.</a>  Note that the provided “main.cpp” requires C++17; see page 6 of this document for more info on enabling C++17.

<h2>Input Files and Processing</h2>

The input files are all .csv files (comma-separated files).  If you double-click they will open in Excel, which is not that helpful.  Better to open in a text editor so you can see what the file actually looks like.  There are two sets of files.  The first set are daily reports put together by John Hopkins university.  Keep in mind this is real data, and real data is often messy.  <u>Example</u>: the names of countries are constantly changing, such as “Mainland China” in the early reports is now simply referred as “China”.   Here’s an example of the first daily report file named “01-22-2020.csv”:




<strong>Province/State,Country/Region,Last Update,Confirmed,Deaths,Recovered </strong>

<strong>Anhui,Mainland China,1/22/2020 17:00,1,, </strong>

<strong>Beijing,Mainland China,1/22/2020 17:00,14,, Chongqing,Mainland China,1/22/2020 17:00,6,, . </strong>

<strong>. </strong>

<strong>. </strong>

<strong>,Japan,1/22/2020 17:00,2,, </strong>

<strong>,Thailand,1/22/2020 17:00,2,, </strong>

<strong>,South Korea,1/22/2020 17:00,1,, </strong>




The first row is a header row; input that line and discard it.  The remaining rows are the data rows, and the total # of data rows is unpredictable.  Notice that some rows do not have a province/state, so the first column may be empty.  And right now most of the last 2 columns are empty — there are no deaths or recovered to report.  For missing confirmed, deaths, or recovered, use 0.  The date of the report can be obtained from the filename, or from the last update column; I prefer the filename because it has the leading 0 (better been ordering by date).




For this daily report, you need to accumulate the data by country — i.e. ignore the province/state, and focus on the country.  For each country, sum the confirmed cases, the deaths, and the recovered cases.  Store all 3 sums in a map, using the country name as the key for fast lookup and data accumulation.  You can use 3 different maps, but I would recommend a single map where the country is the key, and the value is a struct that contains the country name and the 3 sums.  <u>Example</u>:  on “01-22-2020”, China had a total of 547 confirmed cases, 17 deaths, and 28 recovered cases.  On “03-18-2020”, China had a total of 81,102 confirmed cases, 3,241 deaths, and 69,755 recovered cases.




There are currently 57 daily report files, which are cleaned up and posted on the course drop box under

<a href="https://www.dropbox.com/sh/49apjz0efhdnukp/AADszPAg3-Ag1CM6suYGuzP9a?dl=0">“</a><a href="https://www.dropbox.com/sh/49apjz0efhdnukp/AADszPAg3-Ag1CM6suYGuzP9a?dl=0">extra</a><a href="https://www.dropbox.com/sh/49apjz0efhdnukp/AADszPAg3-Ag1CM6suYGuzP9a?dl=0">–</a><a href="https://www.dropbox.com/sh/49apjz0efhdnukp/AADszPAg3-Ag1CM6suYGuzP9a?dl=0">credit</a><a href="https://www.dropbox.com/sh/49apjz0efhdnukp/AADszPAg3-Ag1CM6suYGuzP9a?dl=0">–</a><a href="https://www.dropbox.com/sh/49apjz0efhdnukp/AADszPAg3-Ag1CM6suYGuzP9a?dl=0">files</a><a href="https://www.dropbox.com/sh/49apjz0efhdnukp/AADszPAg3-Ag1CM6suYGuzP9a?dl=0">”</a>; the raw data can be downloaded from <a href="https://github.com/CSSEGISandData/COVID-19">https://github.com/CSSEGISandData/COVID</a><a href="https://github.com/CSSEGISandData/COVID-19">–</a><a href="https://github.com/CSSEGISandData/COVID-19">19</a> (using this tool if need be: <a href="https://desktop.github.com/">https://desktop.github.com/</a><a href="https://desktop.github.com/">)</a>.  Each daily report includes the previous, i.e. the report on “01-23-2020” represents the new total # of confirmed, deaths, and recovered cases.  And then “0124-2020” includes that one, and so on for each daily report.  Thus, the last report on “03-18-2020” contains the world-wide totals for confirmed cases, deaths, and recovered cases.  This is what your “totals” command should output, the totals from this last report:










The implication is that your program needs to store these 3 sums — confirmed, deaths, and recovered — for each country, and for each of the 57 dates.  And you need to do this for the general case, i.e. assume N daily reports where N could be in the thousands.  For testing, we’ll release each new daily report as it becomes available, so you can test your program to make sure it’s not tied to the value of 57.  [ <u>Suggestion</u>: use a single map where the key is the country name, and the value is not just a name and 3 sums, but now it’s a name and 1 or more additional data structures to store all the sums for that country.  A map of maps?  A map of vectors?  Since we are accumulating data by country and also date, you want to support fast lookup.  So the most natural data structure to use in these cases is…  This decision will impact the entire program, both in terms of programming, and efficiency. ]




To drive this point home a bit more, we have 2 additional “world facts” files to input and merge with your country data:  populations and life expectancies:  “populations.csv” and “life_expectancies.csv”, respectively.  We’ll let you open and explore these files, but they can also be found on the course dropbox.  These files should be input and stored by country along with your other data.  This information is output when the user enters a country name, such as <strong>Aruba</strong>:







Note that there may be countries in the daily reports that do not appear in the world facts files, e.g. “Reunion” or “Cruise Ship”.  Likewise, there are countries in the world facts files that do not exist in the daily reports, e.g. “European Union”.  This is typical with real data.  If you lookup a world fact for country X and that value cannot be found, use 0.




How to work with .csv files?  Do not download and install outside libraries, since those will not be available when you submit to gradescope.  It’s not too hard to do everything you need from within C++.  First, open and input from a .csv file like any other text file:  use an <strong>ifstream</strong> object, and check to make sure the file was successfully opened (output an error msg and skip the file if it cannot be opened).  Use the <strong>getline()</strong> function to read line-by-line, skipping the first line (header row).  Here’s the loop, assuming <strong>infile</strong> is your file variable:




string line;

<strong>getline</strong>(infile, line);  // skip first line (header row):




<strong>while</strong> (<strong>getline</strong>(infile, line)) {

.

.   .

}




Now, how to process each line?  This is the messy part — all the code that follows goes *inside* the while loop.  First, we have to deal with the fact that some of the file contain extra commas, in particular to deal with US cities and dates (e.g. “Chicago, IL”).  So some of the lines start with “, and if so, we have to change that from say “City, State” to just City State:




if (line[0] == ‘”‘)  // =&gt; province is “city, state”

{

//

// we want to delete the ” on either end of the value, and

// delete the ‘,’ embedded within =&gt; will get city state:

//

line.erase(0, 1);      // delete the leading ”       size_t pos = line.find(‘,’);  // find embedded ‘,’       line.erase(pos, 1);   // delete ‘,’       pos = line.find(‘”‘); // find closing ”       line.erase(pos, 1);   // delete closing ”     }




Okay, now the line has the correct number of commas, and we can start to parse the data into its individual parts.  We use the C++ <strong>stringstream</strong> class to help:




<strong>stringstream</strong> s(line);

string province, country, last_update;     string confirmed, deaths, recovered;

<strong>getline</strong>(s, province, ‘,’);     <strong>getline</strong>(s, country, ‘,’);      <strong>getline</strong>(s, last_update, ‘,’);     <strong>getline</strong>(s, confirmed, ‘,’);     <strong>getline</strong>(s, deaths, ‘,’);     <strong>getline</strong>(s, recovered, ‘,’);

if (confirmed == “”)       confirmed = “0”;     if (deaths == “”)       deaths = “0”;     if (recovered == “”)    recovered = “0”;

if (country == “Mainland China”)  // map to name in the earlier reports:

country = “China”;




At this point, you have the values you need to store / accumulate in the <strong>map</strong>.  Again, use the country as the key so you can merge this data efficiently with any existing data.  If you forget how to use a <strong>map</strong>, there is a section later in this document to summarize the map API.  Use a similar approach to input the data from the world facts files.




WRITE A SINGLE FUNCTON to process a daily report.  And then call this function N times, once for each report.  If you write N separate functions to input the reports, you will receive a 0 on the project (and you may even fail the class :-).  Seriously, you are better than that.




To help you input the daily reports, we are going to use a class that was made available in C++17:

<strong>filesystem</strong>.  Here’s a function that given a folder / directory name, returns the names of all the files in that folder / directory:




//

// getFilesWithinFolder

//

// Given the path to a folder, e.g. “./daily_reports/”, returns  // a vector containing the full pathnames of all regular files // in this folder.  If the folder is empty, the vector is empty.

//

vector&lt;string&gt; getFilesWithinFolder(string folderPath)

{

vector&lt;string&gt; files;




for (const auto&amp; entry : fs::directory_iterator(folderPath)) {     if (entry.is_regular_file()) {       // this gives you just the filename:

// files.push_back(entry.path().filename().string());




// this gives you the full path + filename:

files.push_back(entry.path().string());

}

}

// let’s make sure the files are in alphabetical order, so we process in order by date:

std::sort(files.begin(), files.end());




return files;

}

In your main() program, you’ll call this function as follows:




vector&lt;string&gt; files = <strong>getFilesWithinFolder</strong>(“./daily_reports/”);




for (string filename : files)

{

readOneDailyReport(filename, data); }




where <strong>data</strong> is a map for accumulating the daily reports.  If you are working outside Codio, you’ll need to adjust your compiler settings to specify C++17.  Using g++, you would use the compiler option -std=c++17.  In Visual Studio, you must change a project property:  Project menu, project properties (very bottom of menu?), expand C/C++, Language, change “C++ Language Standard” to “ISO C++ 17”.




The course dropbox will contain a starter “<a href="https://www.dropbox.com/sh/49apjz0efhdnukp/AADszPAg3-Ag1CM6suYGuzP9a?dl=0">main.cpp</a><a href="https://www.dropbox.com/sh/49apjz0efhdnukp/AADszPAg3-Ag1CM6suYGuzP9a?dl=0">”</a> that contains the necessary #include files, this filesystem-based function, and the beginning of main().  Once you have the input files processed, note that the program should output the following stats:










<h2>Program functionality</h2>

The program supports 6 commands, the last of which is a command of your choice.  Since a country’s name may consist of multiple words (e.g. South Korea), you should input commands from the user using <strong>getline</strong>(cin, command):




<ol>

 <li><strong>help</strong></li>

 <li>Lookup and display of data by country <strong>&lt;name&gt;</strong></li>

 <li>List all <strong>countries</strong> in alphabetical order with data from most recent daily report</li>

 <li>List the <strong>top10</strong> countries based on # of confirmed cases</li>

 <li>List the world-wide <strong>totals</strong> (confirmed, deaths, recovered)</li>

 <li>A command of your own choice</li>

</ol>




Please don’t ask us what you should do for #6, it’s up to you — just do something non-trivial.  We encourage you to post your ideas on Piazza to help generate additional ideas.

As of “03-18-2020”, here are the outputs for the <strong>totals</strong> and <strong>top10</strong> commands.  Feel free to use the built-in sort algorithm if you want:













As of “03-18-2020”, for the <strong>countries</strong> command there should be 174 countries output in alphabetical order.  Here are the first and last 20+ countries:
















&lt;&lt; continued on next page &gt;&gt;

Finally, here are a few examples of individual countries.  If the user enters a country that does not exist, output “country or command not found…”.  Here’s some data on <strong>Aruba</strong>.  The latest data comes from the most recent daily report file.  The first confirmed case, and death, is obtained by searching the accumulated data for the first non-zero values (or “none”).  Finally, there are 3 types of timelines:  confirmed, deaths, and recovered.  The user can also enter “n” for none.  The timeline outputs the accumulated data for that country:
















Here’s some data for <strong>China</strong>.  In this case, the timelines show the first and last 7 reports:













If a timeline consists of &gt; 14 entries, then show the first and last 7, otherwise show the complete timeline.  Finally, here’s the data for the US as of “03-18-2020”:



















As mentioned earlier, use <strong>getline</strong>(cin, command) to obtain the user’s input.  This implies you should use this approach when getting additional input from the user, such as the “c/d/r/n” input that determines the type of timeline.





































<h2>map</h2>

We used the <strong>map</strong> data structure in project #03.  It stores (key, value) pairs in a red-black tree that is hidden from you.  There are two ways to use map.  The first is to search / insert using the <strong>[ ]</strong> operator, e.g.




map&lt;keytype, valuetype&gt;<strong> mymap</strong>;

<strong> </strong>

<strong>mymap</strong>[key] = value;  // insert (key, value) in the map




cout &lt;&lt; <strong>mymap</strong>[key] &lt;&lt; endl;  // search by key for the value




This is very easy to use, with one caveat: if you search and the key is not in the map, it is inserted with a default value.  So you generally want to use this approach for searching *only* when you know the key will be found.  To search without inserting a default value, use the map’s <strong>find()</strong> function, which returns an iterator (aka a pointer):




auto <strong>iter</strong> = mymap.<strong>find</strong>(key);  // search by key for the value

if (iter == mymap.end())  // not found:

{ … } else  // found it!

{   cout &lt;&lt; <strong>iter-&gt;first</strong> &lt;&lt; endl;   // this outputs the key   cout &lt;&lt; <strong>iter-&gt;second</strong> &lt;&lt; endl;  // this outputs the value }




We discussed map in class on days 10 and 11; lecture notes are available <a href="https://www.dropbox.com/sh/xlu3yptqbx3t4qn/AADe5FgfIORo9N8enYmi-07_a?dl=0">here</a><a href="https://www.dropbox.com/sh/xlu3yptqbx3t4qn/AADe5FgfIORo9N8enYmi-07_a?dl=0">.</a>

<h2>Requirements</h2>

<ol>

 <li>You must use a <strong>map</strong> where country name is the key; what the map contains for its value is up to you.</li>

 <li>You can open an input file at most once; this applies to both daily reports and world facts files.</li>

 <li>Your main.cpp program file must have a header comment with your name and a program overview. Each function must have a header comment above the function, explaining the function’s purpose, parameters, and return value (if any).  Inline comments should be supplied as appropriate.</li>

 <li>You must have a single function for inputting a daily report, and call this function N times, once per daily report. Each command must be implemented using a function, and each function should be &lt; 100 lines of code.  This implies a complete solution must have at least 8 functions.</li>

 <li>No global variables; use parameter passing and function return.</li>

 <li>The <strong>cyclomatic complexity</strong> (CCN) of any function may not exceed 15, including main(). This will be reported when you submit on Gradescope, and you’ll be warned if you exceed this threshold.  In short, cyclomatic complexity is a representation of code complexity — e.g. nesting of loops, nesting of if-statements, etc.  You should strive to keep code as simple as possible, which generally means encapsulating complexity within functions instead of explicitly nesting code.  Here’s an example of simpler code with low CCN:</li>

</ol>




while (…) {

if (searchFunctionFindsWhatWeNeed(…))      doSomething();




next value;

}




Here’s an example of complex code with high CCN:




<strong>while</strong> (…) {

<strong>for</strong> (…)  // loop to do search

{

if (search condition is met)

{          <strong>for</strong> (…) // now do something:

{

…

}

}

}                next value;

}




As a general principle, if we see code that has <strong>more than 2 levels</strong> of explicit looping — an example of which is shown above — we will score that code as 0, even if it’s technically correct.

The solution is to move one or more loops into a function, and call the function.

<h2>Grading, electronic submission, and Gradescope</h2>

<strong><u>Submission</u></strong>:  “main.cpp” + additional .cpp, .h, and .hpp files that you submit




This is an extra credit project.  To be eligible, you must have completed Project #05 (threaded AVL trees) by Sunday 3/22 (11:59pm) with an autograder score of 100.  Then, if you successfully complete this project (i.e. score 100 on the autograder), then the final score on this project can be used to replace your lowest project score from projects 1-5.  If it turns out your final score on this project is lower than your project scores on 1-5, then we’ll use this score to replace your lowest 2 HW and lab scores.  If it turns out your final score on this project is lower than all your HW and lab scores, it will be ignored.  Do not ask to apply your score here to the midterm, it will not happen.




Your score on this project is based on two factors:  (1) correctness as determined by your Gradescope submission, and (2) manual review by the TAs for commenting, style, and approach (e.g. use of functions and efficiency of solution).  The entire project is worth 150 points:  100 points for correctness, and 50 points for commenting, style, and approach.  The TAs will also review for adherence to requirements; breaking a requirement can result in a final score of 0 out of 150.  We take all requirements seriously.




By default, we grade your <strong><u>last</u></strong> submission.  Gradescope keeps a complete submission history, so you can <strong><u>activate</u></strong> an earlier submission if you want us to grade a different one; this must be done before the due date.  We assume *every* submission on your Gradescope account is your own work; do not submit someone else’s work for any reason, otherwise it will be considered academic misconduct.




<h2>Policy</h2>

Late work is not accepted since this is an extra-credit project.




All work submitted for grading *must* be done individually.  While we encourage you to talk to your peers and learn from them (e.g. your “iClicker teammates”), this interaction must be superficial with regards to all work submitted for grading.  This means you *cannot* work in teams, you cannot work side-by-side, you cannot submit someone else’s work (partial or complete) as your own.  The University’s policy is available here:




<a href="https://dos.uic.edu/conductforstudents.shtml">https://dos.uic.edu/conductforstudents.shtml</a> .




In particular, note that you are guilty of academic dishonesty if you <u>extend or receive any kind of unauthorized</u> <u>assistance</u>.  Absolutely no transfer of program code between students is permitted (paper or electronic), and you may not solicit code from family, friends, or online forums.  Other examples of academic dishonesty include emailing your program to another student, copying-pasting code from the internet, working in a group on a homework assignment, and allowing a tutor, TA, or another individual to write an answer for you.  It is also considered academic dishonesty if you click someone else’s iClicker with the intent of answering for that student, whether for a quiz, exam, or class participation.  Academic dishonesty is unacceptable, and penalties range from a letter grade drop to expulsion from the university; cases are handled via the official student conduct process described at <a href="https://dos.uic.edu/conductforstudents.shtml">https://dos.uic.edu/conductforstudents.shtml</a> .





