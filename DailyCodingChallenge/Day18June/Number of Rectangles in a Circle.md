## Given a circular sheet of radius, r. Find the total number of rectangles with integral length and width that can be cut from the sheet that can fit on the circle, one at a time.

### Examples :

Input: r=1
Output: 1

Explanation: Only 1 rectangle of dimensions 1x1.

Input: r=2
Output: 8

Explanation: The 8 possible rectangles are 
(1x1)(1x2)(1x3)(2x1)(2x2)(2x3)(3x1)(3x2).

Expected Time Complexity: O(r2)

Expected Auxillary Space: O(1)


Constraints:
1<=r<=1000 


To solve this problem, you need to check for every possible pair of integer lengths and widths whether the rectangle can fit inside the given circle of radius 
# Rectangles in a Circle

Given a circular sheet of radius, \(r\), we want to find the total number of rectangles with integral length and width that can be cut from the sheet, one at a time.

## Formula

The diagonal \(d\) of a rectangle with length \(l\) and width \(w\) is given by the Pythagorean theorem:

$$
d = \sqrt{l^2 + w^2}
$$

To fit the rectangle inside the circle, the diagonal must be less than or equal to the diameter of the circle, \(2r\). Therefore, the condition becomes:

$$
\sqrt{l^2 + w^2} \leq 2r
$$

Squaring both sides to remove the square root:

$$
l^2 + w^2 \leq 4r^2
$$

## C++ Code

Here is the C++ code to count all such rectangles:

```cpp
#include <iostream>
using namespace std;

class Solution {
public:
    int rectanglesInCircle(int r) {
        int count = 0;
        int diameterSquared = 4 * r * r;
        
        for (int a = 1; a <= 2 * r; a++) {
            for (int b = 1; b <= a; b++) { // Ensure b <= a to avoid duplicate counting
                if (a * a + b * b <= diameterSquared) {
                    if (a == b) {
                        count++; // Perfect square, only count once
                    } else {
                        count += 2; // Count both (a, b) and (b, a)
                    }
                }
            }
        }
        return count;
    }
};

int main() {
    Solution solution;
    int r = 5; // Example radius, you can change it as needed
    cout << "Total rectangles: " << solution.rectanglesInCircle(r) << endl;
    return 0;
}

```


you can solve this equation by this way but it is not optimized it only care to work on one condition length , bredth , diagonal <= diameter then it only count that rectangle as a valid rectangle inside define circle radius.

# Rectangles in a Circle

## c++ code

```cpp
#include <iostream>
using namespace std;

class RectanglesInCircle {
public:
    static int countRectangles(int r) {
        int count = 0;
        int radiusSquared = r * r;
        int diameterSquared = 4 * radiusSquared;
        
        // Iterate through all possible lengths and widths
        for (int length = 1; length <= 2 * r; length++) {
            for (int width = 1; width <= 2 * r; width++) {
                // Check if the rectangle's diagonal fits within the circle
                if (length * length + width * width <= diameterSquared) {
                    count++;
                }
            }
        }
        
        return count;
    }
};

int main() {
    int r = 5; // Example radius, you can change it as needed
    cout << "Total rectangles: " << RectanglesInCircle::countRectangles(r) << endl;
    return 0;
}
```