Given a string S, task is to print all permutations of a given string in lexicographically sorted order in C
Permutations of a given string in lexicographically sorted order in C
Here, in this page we will discuss the program to print all permutations of a given string in lexicographically sorted order in C Programming language. We are given with string and need to print them.

Permutations of a given string
Example :
Input : ABC
Output :“ABC, ACB, BAC, BCA, CAB, CBA”

Algorithm :
Sort the given string in non-decreasing order and print it.
The first permutation is always the string sorted in non-decreasing order.
Start generating next higher permutation.
Repeat it until next higher permutation is not possible.
If we reach a permutation where all characters are sorted in non-increasing order, then that permutation is the last permutation.
Permutations of a string in lexicographically sorted order in C
Code in C
Run
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int compare (const void *a, const void * b)
{ return ( *(char *)a - *(char *)b ); }

void swap (char* a, char* b)
{
    char t = *a;
    *a = *b;
    *b = t;
}

int findCeil (char str[], char first, int l, int h)
{
    int ceilIndex = l;
 
    for (int i = l+1; i <= h; i++)
    if (str[i] > first && str[i] < str[ceilIndex])
            ceilIndex = i;
 
    return ceilIndex;
}

void sortedPermutations ( char str[] )
{
    int size = strlen(str);
 
    qsort( str, size, sizeof( str[0] ), compare );
 
    int isFinished = 0;
    while ( ! isFinished )
    {
        printf ("%s \n", str);
 
        int i;
        for ( i = size - 2; i >= 0; --i )
        if (str[i] < str[i+1])
            break;
 
        if ( i == -1 )
            isFinished = 1;
        else{
          
            int ceilIndex = findCeil( str, str[i], i + 1, size - 1 );
            swap( &str[i], &str[ceilIndex] );
            qsort( str + i + 1, size - i - 1, sizeof(str[0]), compare );
        }
    }
}

int main()
{
    char str[] = "ABC";
    sortedPermutations( str );
    return 0;
}
Output :
ABC 
ACB 
BAC 
BCA 
CAB 
CBA 
