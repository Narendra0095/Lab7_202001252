# Lab7_202001252
IT 314
Software Engineering
Lab 7

Name: Narendra Nandaniya
Id: 202001252
Date: 18/04/23

## Program testing using Equivalence Partitioning and Boundary Value Analysis.

### Section A:
### Consider a program for determining the previous date. Its input is triple of day, month and year with the following ranges 1 <= month <= 12, 1 <= day <= 31, 1900 <= year <= 2015.The possible output dates would be previous date or invalid date. Design the equivalence class test cases?

Test suite for the given discription:
Equivalence partitioning:

i) Valid Dates: Dates must follow the given criteria i.e. day, month, year are set to be valid

Thus, all the dates falling between 2/1/1900 and 31/12/2015

(since output of 1/1/1900 will lead to an invalid output)

Ex:

&ensp; 20/10/2005 
&ensp; 12/12/2015
&ensp; 4/5/1985

ii) Invalid Dates: Dates that are not in the criteria given i.e. all the dates falling beyond 31/12/2015 and earlier than 2/1/1900

Ex:

&ensp; 1/1/1900 
&ensp; 2/1/2016
&ensp; 22/5/1895

iii) Boundary Value Dates: the boundary for the program



### P1. The function linearSearch searches for a value v in an array of integers a. If v appears in the array a, then the function returns the first index i, such that a[i] == v; otherwise, -1 is returned.

        int linearSearch(int v, int a[])
        {
            int i = 0;
            while (i < a.length)
            {
                if (a[i] == v)
                return(i);
                i++;
            }
            return (-1);    
        }

| Tester Action and Input Data | Input Value (v)        | Expected Outcome |
|------------------------------|------------------------|------------------|
| Vaild Partition              |                        |                  |
| [1, 2, 3, 4, 5]              | 4                      | 3                |
| [5, 1, 5, 0, 2]              | 0                      | 3                |
| [5, 1, 5, 0, 2]              | 5                      | 0                |
| Invalid Partition            |                        |                  |
| [1, 2, 3, 4, 5]              | -1.5                   | error            |
| [1, 2, 3, 4, 5]              | INT_MAX+1 or INT_MIN-1 | error            |
| [1, 2, 3, 4, 5]              | 1.5                    | error            |
| [ ]                           | 2                      | error            |
| [1, 2, 3, 4, 5]              | null                   | error            |
| Boundary Partition           |                        |                  |
| [1, 2, 3, 4, INT_MAX]        | INT_MAX                | 4                |
| [1, 2, 3, 4, INT_MIN]        | INT_MIN                | 4                |


### P2. The function countItem returns the number of times a value v appears in an array of integers a.
    int countItem(int v, int a[])
    {
        int count = 0;
        for (int i = 0; i < a.length; i++)
        {
            if (a[i] == v)
            count++;
        }
        return (count);
    }

|Tester Action and Input Data|Input Value (v)       |Expected Outcome|
|----------------------------|----------------------|----------------|
|Vaild Partition             |                      |                |
|[1, 3, 2, 3, 4]             |3                     |2               |
|[5, 1, 5, 0, 2]             |0                     |1               |
|[5, 1, 4, 0, 1]             |2                     |0               |
|[-5, 1,- 5, 0, 2]           |-5                    |2               |
|Invalid Partition           |                      |                |
|[1, 2, 3, 4, 5]             |-1.2                  |error           |
|[1, 2, 3, 4, 5]             |INT_MAX+1 or INT_MIN-1|error           |
|[1, 2, 3, 4, 5]             |1.5                   |error           |
|[ ]                          |2                     |error           |
|[1, 2, 3, 4, 5]             |null                  |error           |
|Boundary Partition          |                      |                |
|[1, 2, 3, 4, INT_MAX]       |INT_MAX               |1               |
|[1, 2, 3, 4, INT_MIN]       |INT_MIN               |1               |


### P3. The function binarySearch searches for a value v in an ordered array of integers a. If v appears in the array a, then the function returns an index i, such that a[i] == v; otherwise, -1 is returned.
Assumption: the elements in the array a are sorted in non-decreasing order.

    int binarySearch(int v, int a[])
    {
        int lo,mid,hi;
        lo = 0;
        hi = a.length-1;
        while (lo <= hi)
        {
            mid = (lo+hi)/2;
            if (v == a[mid])
            return (mid);
            else if (v < a[mid])
            hi = mid-1;
            else
            lo = mid+1;
        }
        return(-1);
    }
    
|Tester Action and Input Data            |Input Value (v)    |Expected Outcome|
|----------------------------------------|-------------------|----------------|
|Vaild Partition                         |                   |                |
|[1, 2, 3, 4, 5]                         |2                  |1               |
|[-5,- 3, 0, 2, 3]                       |0                  |2               |
|[-5,- 3, 0, 2, 3]                       |-3                 |1               |
|Invalid Partition                       |                   |                |
|[1, 2, 3, 4, 5]                         |-1.2               |error           |
|[1, 2, 3, 4, 5]                         |1.5                |error           |
|[ ]                                      |2                  |error           |
|[1, 2, 3, 4, 5]                         |null               |error           |
|[1, 2, 3, 4, 5,...]   a.length>INT_MAX/2|                   |error           |
|Boundary Partition                      |                   |                |
|a.length=INT_MAX/2                      |v at the last index|index v         |
|[1, 2, 3, 4, INT_MAX]                   |INT_MAX            |4               |
|[1, 2, 3, 4, INT_MIN]                   |INT_MIN            |4               |


### P4. The following problem has been adapted from The Art of Software Testing, by G. Myers (1979). The function triangle takes three integer parameters that are interpreted as the lengths of the sides of a triangle. It returns whether the triangle is equilateral (three lengths equal), isosceles (two lengths equal), scalene (no lengths equal), or invalid (impossible lengths).

    final int EQUILATERAL = 0;
    final int ISOSCELES = 1;
    final int SCALENE = 2;
    final int INVALID = 3;
    int triangle(int a, int b, int c)
    {
        if (a >= b+c || b >= a+c || c >= a+b)
        return(INVALID);
        if (a == b && b == c)
        return(EQUILATERAL);
        if (a == b || a == c || b == c)
        return(ISOSCELES);
        return(SCALENE);
    }

Equivalennce partition classes:

i) valid class
&ensp; For any value of a, b, c the sum of any two will always be greater than the third, which are further catagorized in three cases

|a  |b  |c  |Expected Outcome |
|---|---|---|-----------------|
|5  |5  |5  |0 (EQUILATERAL)  |
|5  |4  |4  |1 (ISOSCELES)    |
|5  |4  |3  |2 (SCALENE)      |

ii) invalid class
&ensp; For any of the case where any two of a, b, c are smaller than the third the triangle is invalid

|a  |b  |c  |Expected Outcome|
|---|---|---|----------------|
|5  |11  |5  |3 (INVALID)  |
|0  |0  |0  |error    |

iii) boundary class
|a  |b  |c  |Expected Outcome |
|---|---|---|-----------------|
|5  |10  |5  |3 (INVALID)  |
|5  |5  |5  |0 (EQUILATERAL)    |
|5  |4  |4  |1 (ISOSCALES)      |
|5  |4  |3  |2 (SCALENE)      |

### P5. The function prefix (String s1, String s2) returns whether or not the string s1 is a prefix of string s2 (you may assume that neither s1 nor s2 is null).
    public static boolean prefix(String s1, String s2)
    {
        if (s1.length() > s2.length())
        {
            return false;
        }

        for (int i = 0; i < s1.length(); i++)
        {
            if (s1.charAt(i) != s2.charAt(i))
            {
                return false;
            }
        }
        return true;
    }



### P6: Consider again the triangle classification program (P4) with a slightly different specification: The programreads floating values from the standard input. The three values A, B, and C are interpreted asrepresenting the lengths of the sides of a triangle. The program then prints a message to the standard output that states whether the triangle, if it can be formed, is scalene, isosceles, equilateral, or right angled.
Determine the following for the above program:

a) Identify the equivalence classes for the system

Equivalence Classes:
EC1: All sides are positive, real numbers.
EC2: One or more sides are negative or zero.
EC3: The sum of the lengths of any two sides is less than or equal to the length of the remaining side (impossible lengths).
EC4: The sum of the lengths of any two sides is greater than the length of the remaining side (possible lengths).

b) Identify test cases to cover the identified equivalence classes. Also, explicitly mention which test case would cover which equivalence class.
(Hint: you must need to be ensure that the identified set of test cases cover all identified equivalence classes)

Test cases:
TC1 (EC1): A=3, B=4, C=5 (right-angled triangle)
TC2 (EC1): A=5, B=5, C=5 (equilateral triangle)
TC3 (EC1): A=5, B=6, C=7 (scalene triangle)
TC4 (EC1): A=5, B=5, C=7 (isosceles triangle)
TC5 (EC2): A=-2, B=4, C=5 (invalid input)
TC6 (EC2): A=0, B=4, C=5 (invalid input)

c) For the boundary condition A + B > C case (scalene triangle), identify test cases to verify the boundary.

Test cases for the boundary condition A + B > C:
TC7 (EC4): A=2, B=3, C=6 (sum of A and B is equal to C)

d) For the boundary condition A = C case (isosceles triangle), identify test cases to verify the boundary.

Test cases for the boundary condition A = C:
TC8 (EC4): A=5, B=6, C=5 (A equals to C)

e) For the boundary condition A = B = C case (equilateral triangle), identify test cases to verify the boundary.

Test cases for the boundary condition A = B = C:
TC9 (EC4): A=1, B=1, C=1 (all sides are equal)

f) For the boundary condition A2 + B2 = C2 case (right-angle triangle), identify test cases to verify the boundary.

Test cases for the boundary condition A^2 + B^2 = C^2:
TC10 (EC4): A=3, B=4, C=5 (right-angled triangle)

g) For the non-triangle case, identify test cases to explore the boundary.

Test cases for the non-triangle case:
TC11 (EC3): A=2, B=2, C=4 (sum of A and B is less than C)

h) For non-positive input, identify test points.

Test points for non-positive input:
TP1 (EC2): A=0, B=4, C=5 (invalid input)
TP2 (EC2): A=-2, B=4, C=5 (invalid input)
Note: Test cases TC1 to TC10 covers all identified equivalence classes.

## Section B:
#### The code below is part of a method in the ConvexHull class in the VMAP system. The following is a small fragment of a method in the ConvexHull class. For the purposes of this exercise you do not need to know the intended function of the method. The parameter p is a Vector of Point objects, p.size() is the size of the vector p, (p.get(i)).x is the x component of the i th point appearing in p, similarly for (p.get(i)).y. This exercise is concerned with structural testing of code and so the focus is on creating test sets that satisfy some particular coverage criterion.

1. Control Flow diagram:

<img src="https://user-images.githubusercontent.com/84453061/231549750-ee25cbed-d1a8-47f9-8d23-139bea2c2df1.png" width="276" height="740">

2. Test sets:

a) Statement coverage test sets: To achieve statement coverage, we need to make sure that every statement in the code is executed at least once.

Test 1: p = empty vector

Test 2: p = vector with one point

Test 3: p = vector with two points with the same y component

Test 4: p = vector with two points with different y components

Test 5: p = vector with three or more points with different y components

Test 6: p = vector with three or more points with the same y component

b) Branch coverage test sets: To achieve branch coverage, we need to make sure that every possible branch in the code is taken at least once

Test 1: p = empty vector

Test 2: p = vector with one point

Test 3: p = vector with two points with the same y component

Test 4: p = vector with two points with different y components

Test 5: p = vector with three or more points with different y components, and none of them have the same x component

Test 6: p = vector with three or more points with the same y component, and some of them have the same x component

Test 7: p = vector with three or more points with the same y component, and all of them have the same x component

c) Basic condition coverage test sets: To achieve basic condition coverage, we need to make sure that every basic condition in the code (i.e., every Boolean subexpression) is evaluated as both true and false at least once

Test 1: p = empty vector

Test 2: p = vector with one point

Test 3: p = vector with two points with the same y component, and the first point has a smaller x component

Test 4: p = vector with two points with the same y component, and the second point has a smaller x component

Test 5: p = vector with two points with different y components

Test 6: p = vector with three or more points with different y components, and none of them have the same x component

Test 7: p = vector with three or more points with the same y component, and some of them have the same x component

Test 8: p = vector with three or more points with the same y component, and all of them have the same x component.
