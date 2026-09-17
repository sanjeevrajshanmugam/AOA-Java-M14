
# EX 4A Kadane's Algorithm - Dynamic Programming. 

## AIM:
To Write a Java program to solve the below problem using Kadane's Algorithm.
A solar company installs solar panels around a circular grid of n buildings. Each building either generates or consumes net energy, represented by integers (+ve for generated, -ve for consumed).

## Algorithm
1. Input Reading:
Read the number of solar panels n and their corresponding energy values into an integer array energy[].
2. Total Energy Calculation:
Compute the total sum of all energy values, as it will be used to determine the circular subarray case.
3. Find Maximum Subarray Sum (Non-Circular Case):
Use Kadane’s Algorithm to find the maximum subarray sum (maxSum) — representing the best energy output without wrapping around.
4. Find Minimum Subarray Sum (To Handle Circular Case):
Use a modified Kadane’s Algorithm to find the minimum subarray sum (minSum).
The maximum circular energy can then be calculated as wrappedDifference = totalSum - minSum. 
5.  Determine Final Maximum Energy:
If all values are negative, return maxSum (since wrapping gives no benefit).
Otherwise, return the maximum of maxSum and wrappedDifference. 

## Program:
```
Developed by: SANJEEV RAJ S
Register Number:212223220096
import java.util.*;

public class SolarEnergyMaximizer {

    public static int maxCircularEnergy(int[] energy)     {
        
        int sum=0;
        for(int i: energy){
            sum+=i;
        }
        int maxSum=maxSubArraySum(energy);
        int minSum=minSubArraySum(energy);
        int wrappedDifference=sum-minSum;
        if(maxSum<0) return maxSum;
        return Math.max(maxSum,wrappedDifference);
        
    }
    
    public static int maxSubArraySum(int[] energy){
        int sum=0,maxSum=energy[0];
        for(int i:energy){
            sum+=i;
            if(sum>maxSum){
                maxSum=sum;
            }
            if(sum<0) sum=0;
        }
        return maxSum;
    }
    
    public static int minSubArraySum(int[] energy){
        int sum=0,minSum=energy[0];
        for(int i:energy){
            sum+=i;
            if(sum<minSum) minSum=sum;
            if(sum>0) sum=0;
        }
        return minSum;
    }

    
    

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] energy = new int[n];
        for (int i = 0; i < n; i++) {
            energy[i] = sc.nextInt();
        }
        System.out.println(maxCircularEnergy(energy));
    }
}
 

```

## Output:
<img width="500" height="249" alt="image" src="https://github.com/user-attachments/assets/d8c296f3-457a-4519-8fc9-0bd73edf3864" />



## Result:
The program successfully Implemented and the output is verified. 


# EX 4B Frog Jump - Dynamic Programming.

## AIM:
To write a Java program to for given constraints.
A Frog Jump 1 or 2 steps at a time.

## Algorithm
1. Input Reading:
Read an integer n representing the number of steps the frog needs to reach.
2. Base Condition:
If n ≤ 1, return 1 since the frog can reach step 0 or 1 in only one way.
3. Dynamic Programming Setup:
Create an array dp[] of size n + 1, where dp[i] stores the number of ways to reach the ith step. 
4. State Transition:
For each step i from 2 to n, compute
dp[i] = dp[i - 1] + dp[i - 2],
since the frog can jump either 1 or 2 steps at a time. 
5.  Result Output:
The total number of ways to reach the nth step is stored in dp[n] — print this value as the final answer. 

## Program:
```
Developed by: SANJEEV RAJ S
Register Number:212223220096
import java.util.Scanner;

public class FrogJump {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        scanner.close();
        System.out.println(countWays(n));
    }

    public static int countWays(int n) {
        if (n <= 1) return 1;
        int[] dp = new int[n + 1];
        dp[0] = 1;
        dp[1] = 1;
        for (int i = 2; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n];
    }
}

```

## Output:
<img width="440" height="203" alt="image" src="https://github.com/user-attachments/assets/08f0798e-a9a5-4b0a-b9cb-89d3e40238bc" />



## Result:
The program successfully implemented and the expected output is verified.


# EX 4C Coin Change Problem - Dynamic Programming.

## AIM:
To write a Java program to for given constraints.
You are given an integer array coins representing coins of different denominations and an integer amount representing a total amount of money.

Return the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

You may assume that you have an infinite number of each kind of coin.

## Algorithm
1. Input Reading:
Read the list of coin denominations and the target amount to make.
2. Initialization:
Create a dp[] array of size amount + 1, where dp[i] represents the minimum number of coins needed to make amount i.
Initialize all values to a large number (amount + 1), and set dp[0] = 0 (0 coins needed to make amount 0).
3. Dynamic Programming Iteration:
For each amount i from 1 to amount, check every coin value.
If the coin value ≤ i, update
dp[i] = min(dp[i], dp[i - coin] + 1).
4.  Result Check:
After filling the array, if dp[amount] > amount, it means the target amount cannot be formed — return -1.
5.  Output the Result:
Otherwise, print dp[amount], the minimum number of coins needed to make the given amount. 

## Program:
```
Developed by: SANJEEV RAJ S
Register Number:212223220096
import java.util.*;

public class Solution {
    public int coinChange(int[] coins, int amount) {
        int max=amount+1;
        int[] dp=new int[amount+1];
        Arrays.fill(dp,max);
        dp[0]=0;
        for(int i=1;i<=amount;i++){
            for(int coin:coins){
                if(coin<=i){
                    dp[i]=Math.min(dp[i],dp[i-coin]+1);
                }
            }
        }
        return dp[amount]>amount?-1:dp[amount];
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Solution solution = new Solution();
        String coinsLine = scanner.nextLine(); 
        String amountLine = scanner.nextLine();
        coinsLine = coinsLine.replaceAll("[^0-9,]", ""); 
        String[] coinsStr = coinsLine.split(",");
        int[] coins = new int[coinsStr.length];
        for (int i = 0; i < coinsStr.length; i++) {
            coins[i] = Integer.parseInt(coinsStr[i]);
        }
        int amount = Integer.parseInt(amountLine.replaceAll("[^0-9]", ""));
        int result = solution.coinChange(coins, amount);
        System.out.println(result);

        scanner.close();
    }
}
 

```

## Output:
<img width="581" height="248" alt="image" src="https://github.com/user-attachments/assets/80bab794-9297-4027-9dd0-9f16e7c5f147" />



## Result:
The program successfully implemented and the expected output is verified.


# EX 4D Longest Common SubSequence - Dynamic Programming.

## AIM:
To write a Java program to for given constraints.
Given two strings text1 and text2, return the length of their longest common subsequence. If there is no common subsequence, return 0.
A subsequence of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.


## Algorithm
1. Input Reading:
Read two strings text1 and text2 whose longest common subsequence needs to be found.
2. Initialization:
Create a 2D array dp[m+1][n+1], where m and n are lengths of the two strings.
Each dp[i][j] will store the length of the LCS of the first i characters of text1 and first j characters of text2.
3. Dynamic Programming Filling:
Traverse both strings using nested loops.
If text1[i-1] == text2[j-1], then dp[i][j] = dp[i-1][j-1] + 1.
Otherwise, dp[i][j] = max(dp[i-1][j], dp[i][j-1]).
4.  Result Extraction:
After filling the table, the value dp[m][n] represents the length of the longest common subsequence.
5. Output:
Print dp[m][n] as the length of the Longest Common Subsequence.  

## Program:
```

Developed by: SANJEEV RAJ S
Register Number:212223220096
import java.util.Scanner;

public class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        int m = text1.length();
        int n = text2.length();
        int[][] dp = new int[m + 1][n + 1];
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (text1.charAt(i - 1) == text2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                } else {
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }
        return dp[m][n];
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Solution sol = new Solution();
        String text1 = sc.nextLine().replaceAll("\"", "");
        String text2 = sc.nextLine().replaceAll("\"", "");
        int lcsLength = sol.longestCommonSubsequence(text1, text2);
        System.out.println("Length of Longest Common Subsequence: " + lcsLength);
        sc.close();
    }
}


```

## Output:
<img width="1018" height="261" alt="image" src="https://github.com/user-attachments/assets/bd5e00e8-2851-451d-87cf-75b1588afdac" />



## Result:
The program successfully implemented and the expected output is verified.


# EX 4E Longest Increasing Subsequence - Dynamic Programming.

## AIM:
To write a Java program to for given constraints.
Given an integer array nums, return the length of the longest strictly increasing subsequence.

## Algorithm
1. Input Reading:
Read the number of elements n and the array nums[] containing integers.
2. Initialization:
Create an array dp[] of size n and initialize all values to 1 (each element is an LIS of length 1 by itself).
3. Dynamic Programming Update:
For each element nums[i] (from index 1 to n-1),
compare it with all previous elements nums[j] (where 0 ≤ j < i).
If nums[i] > nums[j], then update dp[i] = max(dp[i], dp[j] + 1).
4.  Find Maximum Length:
After filling the dp[] array, the length of the longest increasing subsequence is the maximum value in dp[].
5.  Output:
Print the maximum LIS length as the final result. 

## Program:
```

Program to implement Reverse a String
Developed by: SANJEEV RAJ S
Register Number:212223220096
import java.util.*;

public class LongestIncreasingSubsequence {

    public static int lengthOfLIS(int[] nums) {
        int[] dp=new int[nums.length];
        Arrays.fill(dp,1);
        for(int i=1;i<nums.length;i++){
            for(int j=0;j<i;j++){
                if(nums[i]>nums[j]){
                    dp[i]=Math.max(dp[i],dp[j]+1);
                }
            }
        }
        int longest=0;
        for(int c:dp){
            longest=Math.max(longest,c);
        }
        return longest;
    }

public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

      
        int n = scanner.nextInt();
        int[] nums = new int[n];

        for (int i = 0; i < n; i++) {
            nums[i] = scanner.nextInt();
        }

        
        int result = lengthOfLIS(nums);
        System.out.println("Length of Longest Increasing Subsequence: " + result);

        scanner.close();
    }
}


```

## Output:
<img width="1120" height="241" alt="image" src="https://github.com/user-attachments/assets/1629107c-406e-436d-85c9-549220cdc74a" />



## Result:
The program successfully implemented and the expected output is verified.
