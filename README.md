# counting-sunday
You are given the following information, but you may prefer to do some research for yourself.

1 Jan 1900 was a Monday.
Thirty days has September,
April, June and November.
All the rest have thirty-one,
Saving February alone,
Which has twenty-eight, rain or shine.
And on leap years, twenty-nine.

A leap year occurs on any year evenly divisible by , but not on a century unless it is divisible by .

How many Sundays fell on the first of the month between two dates(both inclusive)?

Input Format

The first line contains an integer , i.e., number of test cases.
Each testcase will contain two lines
 on first line denoting starting date.
 on second line denoting ending date.

Constraints

Output Format

Print the values corresponding to each test case.

Sample Input

2
1900 1 1
1910 1 1
2000 1 1
2020 1 1
Sample Output

18
35
Explanation

For testcase 1, we have the following sundays :-

1 April 1900
1 July 1900
1 September 1901
1 December 1901
1 June 1902
1 February 1903
1 March 1903
1 November 1903
1 May 1904
1 January 1905
1 October 1905
1 April 1906
1 July 1906
1 September 1907 
1 December 1907
1 March 1908
1 November 1908
1 August 1909
-----------------------------------------------------------------------------------------------------------
#include <bits/stdc++.h>
#define LL (long long)
using namespace std;

int Zeller(long long day, long long month, long long year)
{
    if(month < 3) 
    {
        month += 12;
        year--;
    }
    
    long long K = year % 100;
    long long J = LL floor(year / 100);

    return LL(day + LL(floor((13 * (month + 1)) / 5)) + year + LL(floor(year / 4))
            - LL(floor(year / 100)) + LL(floor(year / 400))) % 7; 
}


int main() 
{    
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    
    int t;
    cin >> t;
    
    while(t--)
    {
        long long Y1, M1, D1;
        long long Y2, M2, D2;
        
        cin >> Y1 >> M1 >> D1 >> Y2 >> M2 >> D2;                
        
        if((Y1 > Y2) || (Y1 == Y2 && M1 > M2) || (Y1 == Y2 && M1 == M2 && D1 > D2))
        {
            swap(Y1, Y2);
            swap(M1, M2);
            swap(D1, D2);
        }        
        
        if(D1 > 1) D1 = 1, M1++;
        if(M1 == 13) M1 = 1, Y1++;
        
        long long ans = 0;
        
        while(1)
        {
            int day = Zeller(D1, M1, Y1);
            
            if(day < 0) day += 7;
            if(day == 1) ans++;
            if(Y1 >= Y2 && M1 >= M2) break;
            
            if(M1 == 13) 
            {
                Y1++;
                M1 = 1;
            }
            M1++;                        
        }
        cout << ans << "\n";
    }
}
