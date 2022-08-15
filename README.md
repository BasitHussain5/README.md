# Classification of Data
    #### Video Demo:  <https://www.youtube.com/watch?v=sXB2vfpMBF0>
    #### Description:
Hello world this my CS50 final project. I am Basit Hussain from Gilgit Baltistan Pakistan. My final project is about is about classificatioin of Data. I write some code to make to classify a data of the new student of the university.

So basically in this project I am going to receive one csv file with a data of 10 new students of University. Let's say this file is name is new_student.csv This csv file contains the name of the sudents, Courses of the sudents and date of birth of the sudents. foloeng are the data in new_student.csv.

```
name,courses,birthdate
Aadarsh Mishra,MAT220,2004
Jannat Fatima,CSE110,2008
Ali Hussain,MAT215,2006
Arif Ali,BUS101,2005
Imtiaz Ali,CSE111,2010
Liyaqat Ali,EEE111,2012
Imran Khan,BUS201,2007
Hasan Abbas,BUS120,2009
Tosif Khan,EEE201,2004
Bidhya Bhandari,CSE220,2006
```

Our task is to classify which department they belong to their main courses and select what are their grade according to age. In the end I will create a new csv file that contain these new true classifications depending on their courses that the person has in the csv file we will classify which department they belong to. following are the classify data in after.csv

```
name,department,grade
Aadarsh Mishra,Department of Mthematics and Natural Sciences,Grade 13
Jannat Fatima,Department of Data Sceince,Grade 9
Ali Hussain,Department of Mthematics and Natural Sciences,Grade 11
Arif Ali,Department of Bussiness Administration and management,Grade 12
Imtiaz Ali,Department of Data Sceince,Grade 7
Liyaqat Ali,Department of Electric Engineering,Grade 5
Imran Khan,Department of Bussiness Administration and management,Grade 10
Hasan Abbas,Department of Bussiness Administration and management,Grade 8
Tosif Khan,Department of Electric Engineering,Grade 13
Bidhya Bhandari,Department of Data Sceince,Grade 11
```

Firstly, I import **sys and csv module**. The Python sys module has a number of methods and variables that can be used to modify various elements of the Python runtime environment. Moreover, Python's csv. writer() function can be used to write to a CSV file. The csv. writer() function returns a writer object that creates a delimited string from the user's data.

```
import sys
import csv
```
My project have a main function and three other functions, each of which must be accompanied by tests that can be executed with pytest. My main function be in a file called project.py, which should be in the “root” (i.e., top-level folder) of my project. My three required custom functions other than main must also be in project.py and defined at the same indentation level as main (i.e., not nested under any classes or functions).

```
def main():
    check_correct_args()
    data = []
    try:
        with open(sys.argv[1]) as csvfile:
            reader = csv.DictReader(csvfile)
            for row in reader:
                data.append(row)
    except FileNotFoundError:
        sys.exit("could't read csv file")

    output = []
    for row in data:
        department = select_department(row["courses"])
        grade = select_grade(row["birthdate"])
        output.append({"name": row["name"], "department": department, "grade": grade})

    with open(sys.argv[2], "w") as file:
        writer = csv.DictWriter(file, fieldnames=["name", "department", "grade"])
        writer.writerow({"name": "name", "department": "department", "grade": "grade"})
        for row in output:
            writer.writerow({"name": row["name"], "department": row["department"], "grade": row["grade"]})


def check_correct_args():
    if len(sys.argv) < 3:
        sys.exit("Too few command-line arguments")
    if len(sys.argv) > 3:
        sys.exit("Too many command-line arguments")
    if ".csv" not in sys.argv[1] or ".csv" not in sys.argv[2]:
        sys.exit("Not csv files")


def select_department(char):
    if char in ["CSE110", "CSE111", "CSE220"]:
        return "Department of Data Sceince"
    if char in ["MAT110", "MAT220", "MAT215"]:
        return "Department of Mthematics and Natural Sciences"
    if char in ["BUS101", "BUS201", "BUS120"]:
        return "Department of Bussiness Administration and management"
    elif char in ["EEE201", "EEE111", "EEE301"]:
        return "Department of Electric Engineering"
    else:
        return "NO Department"


def select_grade(year):
    age = 2022 - int(year)
    grade = age - 5
    return "Grade " + str(grade)



if __name__ == "__main__":
    main()
```

In my main function I excute my three other functions, this three function be accompanied by tests that can be executed with pytest. My main function be in a file called project.py, which should be in the “root” (i.e., top-level folder) of my project. My three required custom functions other than main must also be in project.py and defined at the same indentation level as main. 

At first, in the function check_correct_args() we check the length of the sys.argv. if the length less than 3 then its show Too few command-line arguments. if if the length greater than 3 then its show Too many command-line arguments. if ".csv" not in sys.argv[1] or ".csv" not in sys.argv[2] then it show Not csv files In the fuction. Secondly, in the function department_select(char) I check char return the nmae of the department according to the char. After some research I define three main courses of each department. For instance, for the department of computer science we have the courses CSE110, CSE111 and CSE220. For Department of MNS we have MAT110, MAT220, MAT215. For Department of BBA we have BUS101, BUS201, BUS120. And finally for Department of Electrical engineering we have EEE201., EEE111, EEE301. Finally, in the function select_grade(year). To select the grade, we are assuming that every person will start at University according to the grade they should be by their age.  For instance, if some has 13 years this person should be in grade 8.


I test functions in a file called test_project.py, which should also be in the “root” of my project. they have the same name as my custom functions, prepended with test_ (test_custom_function, for example, where custom_function is a function I’ve implemented in project.py).

```
from project import check_correct_args, select_house, select_grade
import pytest

def test_check_correct_args():
    with pytest.raises(SystemExit):
        check_correct_args()



def test_select_department():
    assert select_department("CSE110") == "Department of Computer Sceince"
    assert select_department("MAT110") == "Department of Mthematics and Natural Sciences"
    assert select_department("BUS101") == "Department of Bussiness Administration and management"
    assert select_department("EEE201") == "Department ogf Electric Engineering"


def test_select_grade():
    assert selec_grade(2005) == "Grade 12"
    assert selec_grade(2015) == "Grade 2"

```
