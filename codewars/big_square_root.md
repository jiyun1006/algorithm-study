# 큰수의 Square root를 구하는 방법

big number division 이라는 방법을 사용해 구현하였음.

방법 주소: [Big number division](https://www.freecodecamp.org/news/find-square-root-of-number-calculate-by-hand/)

문제 주소: [CodeWars Big Number Square Root](https://www.codewars.com/kata/58a3fa665973c2a6e80000c4)


## 어떻게 구현하였는지?
1. Big number의 Square root를 구하는 것이기 때문에 string으로 받음.
2. 수의 자리수가 홀수일경우 앞에 0을붙여 짝수로 만들어 줘야함.
3. 해당 방법은 자리수를 2칸씩 읽어 간다.
4. 처음에는 해당 수보다 제곱이 작은 자연수를 찾는다. 예를 들어 2025라면 20보다 작은 제곱을 갖는 최대의 자연수는 4임.
5. 4의 제곱인 16을 빼서 425로 만듬.
6. 이제부터 구한 자연수의 값에 2배를 한후 숫자를 붙여서 그 수를 붙인값이랑 곱한것이 현재 나머지 수보다 같거나 작을때까지 수를 늘림. 85*5 = 425 5일때 만족하게됨.
7. 따라서 45가 2025의 square root가 됨. 
8. 이러한 방식이 나머지수보다 작거나 같아질때까지만 반복함. 만약 더이상 작아질 수 없다면 멈추고 해당 값을 return한다.

### 느낀점
풀이 방법을 모를때는 어려우나 Big number division method를 이해하면 쉬운 문제.
수학적 문제라 실제 코테에서는 나올지 모르겠음.

```c++

#include <vector>
#include <string>
#include <regex>
#include <iostream>
#include <sstream>
#include <cmath>


using namespace std;


string mul(string a, string b)
{
    int len1 = a.size();
    int len2 = b.size();
    if (len1 == 0 || len2 == 0)
        return "0";

    // will keep the result number in vector 
    // in reverse order 
    vector<int> result(len1 + len2, 0);

    // Below two indexes are used to find positions 
    // in result.  
    int i_n1 = 0;
    int i_n2 = 0;

    // Go from right to left in a 
    for (int i = len1 - 1; i >= 0; i--)
    {
        int carry = 0;
        int n1 = a[i] - '0';

        // To shift position to left after every 
        // multiplication of a digit in b 
        i_n2 = 0;

        // Go from right to left in b              
        for (int j = len2 - 1; j >= 0; j--)
        {
            // Take current digit of second number 
            int n2 = b[j] - '0';

            // Multiply with current digit of first number 
            // and add result to previously stored result 
            // at current position.  
            int sum = n1 * n2 + result[i_n1 + i_n2] + carry;

            // Carry for next iteration 
            carry = sum / 10;

            // Store result 
            result[i_n1 + i_n2] = sum % 10;

            i_n2++;
        }

        // store carry in next cell 
        if (carry > 0)
            result[i_n1 + i_n2] += carry;

        // To shift position to left after every 
        // multiplication of a digit in a. 
        i_n1++;
    }

    // ignore '0's from the right 
    int i = result.size() - 1;
    while (i >= 0 && result[i] == 0)
        i--;

    // If all were '0's - means either both or 
    // one of a or b were '0' 
    if (i == -1)
        return "0";

    // generate the result string 
    string s = "";

    while (i >= 0)
        s += std::to_string(result[i--]);

    s = regex_replace(s, regex("^0+"), "");
    return s.length() ? s : "0";


    //return s;
}
bool isSmaller(string str1, string str2)
{
    // Calculate lengths of both string 
    int n1 = str1.length(), n2 = str2.length();

    if (n1 < n2 || n1 == n2 && str1 < str2)
        return true;
    if (n2 < n1 || n1==n2 && str1>str2)
        return false;

    if (str1 == str2)
        return true;

    return false;
}

// Function for find difference of larger numbers 
string sub(string str1, string str2)
{
    // Before proceeding further, make sure str1 
    // is not smaller 
 
    // Take an empty string for storing result 
    string str = "";

    // Calculate length of both string 
    int n1 = str1.length(), n2 = str2.length();
    str1 = string(max(0, n2-n1), '0')+str1;
    str2 = string(max(0, n1-n2), '0')+str2;
    // Reverse both of strings 
    reverse(str1.begin(), str1.end());
    reverse(str2.begin(), str2.end());

    int carry = 0;

    // Run loop till small string length 
    // and subtract digit of str1 to str2 
    for (int i = 0; i < n2; i++)
    {
        // Do school mathematics, compute difference of 
        // current digits 

        int sub = ((str1[i] - '0') - (str2[i] - '0') - carry);

        // If subtraction is less then zero 
        // we add then we add 10 into sub and 
        // take carry as 1 for calculating next step 
        if (sub < 0)
        {
            sub = sub + 10;
            carry = 1;
        }
        else
            carry = 0;

        str.push_back(sub + '0');
    }

    // subtract remaining digits of larger number 
    for (int i = n2; i < n1; i++)
    {
        int sub = ((str1[i] - '0') - carry);

        // if the sub value is -ve, then make it positive 
        if (sub < 0)
        {
            sub = sub + 10;
            carry = 1;
        }
        else
            carry = 0;

        str.push_back(sub + '0');
    }

    // reverse resultant string 
    reverse(str.begin(), str.end());

    str = regex_replace(str, regex("^0+"), "");
    return str.length() ? str : "0";

   // return str;
}



bool iscomp(string a, string b)
{
  
 int len1=a.size();
 int len2=b.size();
  
 a = string(max(0, len2-len1), '0')+a;
 b = string(max(0, len1-len2), '0')+b;

 if(a==b)
   return true;
  for(int i=0;i<a.size();i++)
  {
    if(a[i]<b[i])
      return true;
    else if(a[i]>b[i])
      return false;
  }

}


string integer_square_root(string n) {
  // Coding and coding ... 
 
  
int digits = n.length(), root;
    string result;
    if(digits < 16){
        root = static_cast<int>(floor(sqrt(stoul(n))));
        result = to_string(root);
    }
    // 숫자로 계산이 가능한 경우는 long형 변환
   else
    {
     result="0";
     string carry="0";
     if(digits%2) //홀수면
       n="0"+n;
     
     // hard 메소드를 이용하여 시도
     for(int i=0, len=n.size();i<len;i+=2)
       {
       
       carry+=n.substr(i,2);
       
       string curr2 = mul(result, "2");
       int j=0;
       while(iscomp(mul(curr2+to_string(j), ""+to_string(j)), carry) && j<10)
         j++;
       
       result+=to_string(--j);
       
       carry = sub(carry, mul(curr2+to_string(j), to_string(j)));
       cout<<carry<<endl;
       
       
     }
     
       
     }
     
     
     
     
   result = regex_replace(result, regex("^0+"), "");
   
    
    return result.size()?result:"0";

}









```
