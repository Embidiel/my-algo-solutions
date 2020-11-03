## 1431. Kids With the Greatest Number of Candies

https://leetcode.com/problems/kids-with-the-greatest-number-of-candies/

### Breakdown:
---
***Kunin muna yung initial na pinaka-malaking number of candies na meron sa isang bata.***

Note: `Math.max` accepts only a number of parameters like `Math.max(1,2,3,4)` which equals to 4.

I spread the values using rest operator.

    const maxvalue = Math.max(...candies);

---

***Dito chini-check natin kung magiging mas marami ba yung candies nung isang bata kapag binigay natin yung extra candies.***

           const kids = candies.map(kid => {
            if((kid + extraCandies) >= maxvalue){
                return true;
            } else {
                return false;
            }
        });


---

***Code***

    var kidsWithCandies = function(candies, extraCandies) {
        const maxvalue = Math.max(...candies);
    
        const kids = candies.map(kid => {
            if((kid + extraCandies) >= maxvalue){
                return true;
            } else {
                return false;
            }
        });
        
        return kids;
    };

## 1480. Running Sum of 1d Array

https://leetcode.com/problems/running-sum-of-1d-array

### Breakdown:
---
Gusto natin mangyari dito is ***ma-replace yung current element sa current value na looped sa array***. ***Yung replacement is yung current value tapos added yung current sum.***

***Example:***

    1 = 1 + 0;
    2 =  2 + 1;
    3 = 3 + 3;
    4 = 4 + 6

***Result*** = `[1,3,6,10]`


      for (let i = 0; i < maxlength; i++){
            const num = nums[i]
            nums[i] = num + currentSum;
            currentSum = currentSum + num;
        }


***Code***

    var runningSum = function(nums) {
        let currentSum = 0;
        const maxlength = nums.length;
        for (let i = 0; i < maxlength; i++){
            const num = nums[i]
            nums[i] = num + currentSum;
            currentSum = currentSum + num;
        }
        return nums;
    };
