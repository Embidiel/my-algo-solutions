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
