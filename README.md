# Infix-RPN
Library to convert between Infix and Reverse Polish Notation (RPN) strings

This kata is written in C on Ubuntu 14.04 and uses Git, make, gcc & Check 0.10.0 to develop a simple library that converts an infix string to a Reverse Polish Notation (RPN) string.

Folder structure:
make
   --program.makefile
project
   -- src
      --infixtorpn.c
   -- hdr
      --infixtorpn.h
tst
   --testfile.c

tst/testfile.c contains the structure to set up and run a test to convert one or more infix strings to RPN with the option to output the strings to screen. An example single string test file is shown at the end of this document.

To run the test as per the file/folder structure shown above, open a command prompt / terminal window, navigate to the 'make' directory and run:
   make -f program.makefile test

----------------------------------------------
[testfile.c]
#include <stdio.h> 
#include <stdlib.h>
#include <check.h>
#include "../project/hdr/infixtorpn.h"
 START_TEST(infixToRPN)
 {
     printf("START TEST\n");
     Infix2RPN * i2r;
     i2r = create(1);
     i2r = convert(i2r, "a+b");
     ck_assert_str_eq(getRPN(i2r), "ab+");
     i2r = freeStrings(i2r);
     i2r = freeStruct(i2r);
     printf("END TEST\n");
 }
 END_TEST
 int main(void)
 {
    Suite *s1 = suite_create("Core");
    TCase *tc1_1 = tcase_create("Core");
    SRunner *sr = srunner_create(s1);
    int nf;
    suite_add_tcase(s1, tc1_1);
    tcase_add_test(tc1_1, infixToRPN);
    srunner_run_all(sr, CK_ENV);
    nf = srunner_ntests_failed(sr);
    srunner_free(sr);
    return nf == 0 ? 0 : 1;
 }

----------------------------------------------
[sample infix to RPN strings]
INFIX			            RPN
-----			            ---
a+b	                  ab+
(a+b)-c			          ab+c-
l/m^n*o-p		          lmn^/o*p-
((v/w)^x)*(y-z)		    vw/x^yz-*
