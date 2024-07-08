# Find-the-Winner-of-the-Circular-Game

There are n friends that are playing a game. The friends are sitting in a circle and are numbered from 1 to n in clockwise order. More formally, moving clockwise from the ith friend brings you to the (i+1)th friend for 1 <= i < n, and moving clockwise from the nth friend brings you to the 1st friend.

The rules of the game are as follows:

Start at the 1st friend.
Count the next k friends in the clockwise direction including the friend you started at. The counting wraps around the circle and may count some friends more than once.
The last friend you counted leaves the circle and loses the game.
If there is still more than one friend in the circle, go back to step 2 starting from the friend immediately clockwise of the friend who just lost and repeat.
Else, the last friend in the circle wins the game.
Given the number of friends, n, and an integer k, return the winner of the game.


Example 1:

Input: n = 5, k = 2
Output: 3

Explanation: Here are the steps of the game:
1) Start at friend 1.
2) Count 2 friends clockwise, which are friends 1 and 2.
3) Friend 2 leaves the circle. Next start is friend 3.
4) Count 2 friends clockwise, which are friends 3 and 4.
5) Friend 4 leaves the circle. Next start is friend 5.
6) Count 2 friends clockwise, which are friends 5 and 1.
7) Friend 1 leaves the circle. Next start is friend 3.
8) Count 2 friends clockwise, which are friends 3 and 5.
9) Friend 5 leaves the circle. Only friend 3 is left, so they are the winner.
Example 2:

Input: n = 6, k = 5
Output: 1
Explanation: The friends leave in this order: 5, 4, 6, 2, 3. The winner is friend 1.
 

Constraints:

1 <= k <= n <= 500

# SOLUTION 

# Intuition
Pretty normal and understandable approach which first comes to anyone's mind

We can simulate the circle with array: when we reached the last element in the array we'll go to the first element in the array
Since we want to find original index as elements we would use 1-indexed indeces from original circle
You can find the index (relative in the array) of next player to lose as (cur_ind + k - 1) % n where n is the current size of array

# Coding
Initialize a list circle with integers from 1 to n representing initiall indeces.
Set the initial index cur_ind to 0.
Begin a while loop that continues until the length of circle is 1 (we've found a winner):
Calculate the index next_to_remove of the next person to be removed.
Remove the element at next_to_remove from circle.
Update cur_ind to next_to_remove.
Return the last remaining element in circle (winner original index).

# Complexity Analysis
- Time complexity: O(n^2), since you remove n - 1 friends from circle with pop operation (which is O(n)).
- Space complexity: O(n), since we use additional array of size n - circle

# JAVA CODE

class Solution {

    public int findTheWinner(int n, int k) {

         ArrayList<Integer> circle = new ArrayList<>();
         
        for (int i = 1; i <= n; ++i) {
        
            circle.add(i);
        }
        int cur_ind = 0;

        while (circle.size() > 1) {
        
            int next_to_remove = (cur_ind + k - 1) % circle.size();
            
            circle.remove(next_to_remove);
            
            cur_ind = next_to_remove;
        }

        return circle.get(0);
    }
}
 
