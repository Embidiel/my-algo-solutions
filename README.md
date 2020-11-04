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

## 1512. Number of Good Pairs

https://leetcode.com/problems/number-of-good-pairs/

### Breakdown
---
Una binilang ko muna kung ilang beses lumitaw yung isang number tapos sa array tapos ini-store ko sa isang Hash Map.

***Example*** : `[1,2,3,1,1,3]`;
***Result ng Hash Map***

    {
    	1: 3,
    	2: 1,
    	3: 2
    }

---


    const frequency = nums.reduce((acc, num) => {
            if(!acc[num]) acc[num] = 1;
            else acc[num]++;
            
            return acc;
        }, {});


---

Sa second loop ang ginawa ko is bawat number na naging key na sa Hash Map ay dinaan ko tapos kinuha ko yung value nung key na yun.

       for(const key of keys){
            const n = frequency[key];
            const res =  n * (n - 1) / 2;
            pairs += res;
        }

---
Noticed that I used this formula `n * (n - 1) / 2`.
Explanation photo below:

![enter image description here](https://imgur.com/tC9V9md.png)



---
***Code***

    var numIdenticalPairs = function(nums) {
        let pairs = 0;
        const frequency = nums.reduce((acc, num) => {
            if(!acc[num]) acc[num] = 1;
            else acc[num]++;
            
            return acc;
        }, {});
        
        
        const keys = Object.keys(frequency);
    
        for(const key of keys){
            const n = frequency[key];
            const res =  n * (n - 1) / 2;
            pairs += res;
        }
        
        return pairs;
    }
