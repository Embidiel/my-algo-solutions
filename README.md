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


## 1470. Shuffle the Array

https://leetcode.com/problems/shuffle-the-array/

### Breakdown:
---
Kunin natin yung elements starting from the first element, up to the n na index.

Example : `[1,2,3,4,4,3,2,1]`. Where `n is 4`
Result is `[1,2,3,4]`

    const xs = nums.splice(0, n)

---

Get all elements of the array starting from the last element up to -n.
Example : `[1,2,3,4,4,3,2,1]`. Where `-n is -4`
Result is `[4,3,2,1]`

Note: A `negative integer` given sa `splice` function indicates that you are ***starting from the last item of an array.***

    const ys = nums.splice(-n)

---

Push all elements from xs and ys starting from its first elements. 

    let res = []; 
    for(let x = 0; x < end; x++){
	     res.push(xs[x]); 
	     res.push(ys[x]); 
     }


---

***Code:***

    var shuffle = function(nums, n) {
        const xs = nums.splice(0, n)
        const ys = nums.splice(-n)
        
        const end = xs.length > ys.length ? xs.length : ys.length;
        let res = [];
        for(let x = 0; x < end; x++){
            res.push(xs[x]);
            res.push(ys[x]);
        }
        return res;
    };
