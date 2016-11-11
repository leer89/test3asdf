========================================================================
    CONSOLE APPLICATION : test3asdf Project Overview
========================================================================

AppWizard has created this test3asdf application for you.

This file contains a summary of what you will find in each of the files that
make up your test3asdf application.


test3asdf.vcxproj
    This is the main project file for VC++ projects generated using an Application Wizard.
    It contains information about the version of Visual C++ that generated the file, and
    information about the platforms, configurations, and project features selected with the
    Application Wizard.

test3asdf.vcxproj.filters
    This is the filters file for VC++ projects generated using an Application Wizard. 
    It contains information about the association between the files in your project 
    and the filters. This association is used in the IDE to show grouping of files with
    similar extensions under a specific node (for e.g. ".cpp" files are associated with the
    "Source Files" filter).

test3asdf.cpp
    This is the main application source file.

/////////////////////////////////////////////////////////////////////////////
Other standard files:

StdAfx.h, StdAfx.cpp
    These files are used to build a precompiled header (PCH) file
    named test3asdf.pch and a precompiled types file named StdAfx.obj.

/////////////////////////////////////////////////////////////////////////////
Other notes:

AppWizard uses "TODO:" comments to indicate parts of the source code you
should add to or customize.

/////////////////////////////////////////////////////////////////////////////

MIKE SUP 
THIS GUY GOES HARD
// Authors – Randy Lee, Mike Soper

#include<iostream>
#include <iomanip>  

const int numOfStudents = 5, numOfQuizzes = 4;

void compute_studentAvg(const int grade[][numOfQuizzes], double studentAvg[]);
void compute_quizAvg(const int grade[][numOfQuizzes], double quizAvg[]);
void display(const int grade[][numOfQuizzes], const double studentAvg[], const double quizAvg[]);

int main()
{
	using namespace std;

	int grade[numOfStudents][numOfQuizzes];
	double studentAvg[numOfStudents];
	double quizAvg[numOfQuizzes];

	cout << "... Now filling array ...";
	grade[0][0] = 46; grade[0][1] = 76; grade[0][2] = 14; grade[0][3] = 100;
	grade[1][0] = 64; grade[1][1] = 45; grade[1][2] = 97; grade[1][3] = 78;
	grade[2][0] = 54; grade[2][1] = 56; grade[2][2] = 48; grade[2][3] = 94;
	grade[3][0] = 31; grade[3][1] = 23; grade[3][2] = 12; grade[3][3] = 45;
	grade[4][0] = 86; grade[4][1] = 78; grade[4][2] = 79; grade[4][3] = 82;

	compute_studentAvg(grade, studentAvg);
	compute_quizAvg(grade, quizAvg);
	display(grade, studentAvg, quizAvg);
	return 0;
}

void compute_studentAvg(const int grade[][numOfQuizzes], double studentAvg[])
{
	for (int studentNum = 1; studentNum <= numOfStudents; studentNum++)
	{   //Process one studentNum:
		double sum = 0;
		for (int quizNum = 1; quizNum <= numOfQuizzes; quizNum++)
			sum = sum + grade[studentNum - 1][quizNum - 1];
		
		//sum contains the sum of the quiz scores for student number studentNum.
		
		studentAvg[studentNum - 1] = sum / numOfQuizzes;
		//Average for student studentNum is the value of studentAvg[studentNum-1]
	}
}

void compute_quizAvg(const int grade[][numOfQuizzes], double quizAvg[])
{
	for (int quizNum = 1; quizNum <= numOfQuizzes; quizNum++)
	{   
		//Process one quiz (for all students):
		double sum = 0;
		for (int studentNum = 1; studentNum <= numOfStudents; studentNum++)
			sum = sum + grade[studentNum - 1][quizNum - 1];
		
		//sum contains the sum of all student scores on quiz number quizNum.
		quizAvg[quizNum - 1] = sum / numOfStudents;

		//Average for quiz quizNum is the value of quizAvg[quizNum-1]
	}
}

//Uses iostream and iomanip:
void display(const int grade[][numOfQuizzes],
	const double studentAvg[], const double quizAvg[])
{
	using namespace std;

	cout.setf(ios::fixed);
	cout.setf(ios::showpoint);
	cout.precision(1);

	cout << setw(10) << "Student" << setw(5) << "Ave"
		<< setw(15) << "Quizzes\n";
	for (int studentNum = 1; studentNum <= numOfStudents; studentNum++)
	{
		//Display for one studentNum:
		cout << setw(10) << studentNum << setw(5) << studentAvg[studentNum - 1] << " ";
		for (int quizNum = 1; quizNum <= numOfQuizzes; quizNum++)
			cout << setw(5) << grade[studentNum - 1][quizNum - 1];
		cout << endl;
	}

	cout << "Quiz averages = ";
	for (int quizNum = 1; quizNum <= numOfQuizzes; quizNum++)
		cout << setw(5) << quizAvg[quizNum - 1];
	cout << endl;
}

