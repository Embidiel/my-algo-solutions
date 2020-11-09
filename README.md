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

## 1365. How Many Numbers Are Smaller Than the Current Number

https://leetcode.com/problems/how-many-numbers-are-smaller-than-the-current-number/

### Breakdown
---
I built a nested for loop to traverse the elements multiple times and compare kung mas malaki ba yung current number to the next numbers
and then may counter ako kung ilan yung number na mas maliit sa kanya sa list.

Pag natapos yung isang pass sa array, add lang yung laman ng count
sa array tapos sunod ulit na pass.


***Example :***

    [8,1,2,2,3]

    8 > 2 , 8 > 1, .......
    1 > 8 , 1 > 1, ......

---

    for(let x = 0; x < nums.length ; x++){
        let current = nums[x];
        let count = 0;
        
        for(let y = 0; y < nums.length; y++){
            if(current > nums[y]){
                count++;
            }
        }
        
        res.push(count);
        count = 0;
    }

---


***Code:***

    var smallerNumbersThanCurrent = function(nums) {
    let res = [];
    for(let x = 0; x < nums.length ; x++){
        let current = nums[x];
        let count = 0;
        
        for(let y = 0; y < nums.length; y++){
            if(current > nums[y]){
                count++;
            }
        }
        
        res.push(count);
        count = 0;
    }
	    return res;
    };


## 136. Single Number

https://leetcode.com/problems/single-number/

### Breakdown
---

Gumamit ako dito ng bitwise operator na XOR or ^.
So ginagawa nito is every bits of a given decimal kino-compare and then
***if yung bit 1 is parehas sa bit 2 na compared*** 
***mag re-return to ng*** ***false or 0***

***Example:***

    [4,1,2,1,2]

---

***Bits equivalent***

    4 = 100
    1 = 001
    2 = 010
---

    ***Step 1***
    100 
    001
    ---
	101
    
    ***Step 2***
    101 
    010
    ---
    111
  
    
    ***Step 3***
    111
    001
    ---
    110
    
    ***Step 4***
    
    110
    010
    ---
    100 into decimal is 4


---


    var singleNumber = function(nums) {
        return nums.reduce((acc, num) => acc ^ num, 0)
    };


## 268. Missing Number

https://leetcode.com/problems/missing-number/

---

***Breakdown***

---

First loop, gumawa muna ako ng ***Hash map para ma store yung values na present sa array for easy access sa Second loop.***

Sa Second loop, nag loop ako sa number 0 up to n. 
***If yung present na number or x is wala sa reference Hash Map ibig sabihinsiya yung kulang na value sa sequence.***

---

    var missingNumber = function(nums) {
        
        const nummap = nums.reduce((acc, num) => {
            acc[num] = true;
            return acc;
        }, {});
        
    
        for(let x = 0; x <= nums.length ; x++){
            if(!nummap[x]) return x;
        }
    };


## 1. Two Sum

https://leetcode.com/problems/two-sum/

### Breakdown

---

Sa first loop ang ginawa ko dito is gumawa ako ng Hash Map para ma-store yung number and then yung partner niya na index in a key-value pair.

      const visitedmap = nums.reduce((acc, num, index) => {
                acc[num] = index
                return acc;
            }, {});

---

Sa second loop dinaanan ko ulit yung nums na array this time k***inukuha ko yung difference nung target number tsaka yung current number sa loob ng loop.***

The reason is ***gusto ko makuha yung complement number or partner number for addition sa target number.***

***If present yung complement / diff number sa loob ng Hash Map na ginawa natin previously at hindi siya equal sa sarili niya*** ( Goal natin dito is two different numbers) and then ayun na yung indices na need natin ma-return.

        for(let x = 0; x < nums.length ; x++){
            const diff = target - nums[x];
            if(visitedmap[diff] && visitedmap[diff] !== x){
                return [x, visitedmap[diff]];
            }
        }


---
***Code***

    var twoSum = function(nums, target) {
        const visitedmap = nums.reduce((acc, num, index) => {
            acc[num] = index
            return acc;
        }, {});
    
        
        for(let x = 0; x < nums.length ; x++){
            const diff = target - nums[x];
            if(visitedmap[diff] && visitedmap[diff] !== x){
                return [x, visitedmap[diff]];
            }
        }
    };

## ?. Three Sum

### Breakdown

----
We're sorting the array ***pa ascending order / least to greatest .***


    nums = nums.sort();


---

***At max gusto natin matapos yung pag loop sa array bago mawalan ng tig 3 items***. 

We minus 2 kasi the first one is kailangan sa left pointer and yung another one is needed sa second pointer sa kanan.

     let endloop = nums.length - 2;

---

From the first element gusto natin magsimula yung left pointer or yung second item sa kasunod na element nung current number sa loop.

For example : `[1,2,3,4,5]`

Gusto natin magsimula yung left pointer sa 2.

For the right pointer naman gusto natin magsimula sa pinaka-dulong item which is 5.

     let left = x + 1;
     let right = nums.length - 1;

---
***Habang hindi pa nagcro-cross yung paths ng dalawang pointer continue lang yung loop, otherwise break na yung loop*** kasi nagamit na or nadaanan na lahat ng items sa loob ng array.


    while(left < right)

---

Dito naman ***kinukuha natin yung sum nung  current number, left pointer at right pointer.***

Tapos ***kung yung sum is less than 0 ililipat natin yung left pointer pa-kanan kasi kung mas maliit yung sum sa 0 there's a possibility na makuha natin yung 0 pag nagincrease tayo ng value (sorted kasi yung array na to)***

Pag ***yung sum naman is greater than 0 ibig sabihin naman nito masyadong malayo sa range nung target value natin yung sum kaya 
kailangan i-move natin yung right pointer pa-left para lumiit naman yung sum.***

If yung ***sum naman is equal sa 0 and then nakakuha na tayo ng triplet at need natin to mapasok sa result array.***

     const sum = nums[x] + nums[left] + nums[right];
                 
      if (sum < 0){
           left++;
      } else if (sum > 0){
           right--;
      } else if(sum === 0){
           result.push([nums[x] , nums[left] , nums[right]]);
           left++;
           right--;
     }

---
***Code***


    var threeSum = function(nums) {
        
        if(nums.length < 3){
            return [];
        }
        
        nums = nums.sort();
               
        let result = [];
        let endloop = nums.length - 2;
        
        for(let x = 0; x < endloop; x++){
       
            let left = x + 1;
            let right = nums.length - 1;
            
            while(left < right){
              
                const sum = nums[x] + nums[left] + nums[right];
             
                if (sum < 0){
                    left++;
                } else if (sum > 0){
                    right--;
                }   else if(sum === 0){
                   result.push([nums[x] , nums[left] , nums[right]]);
                   left++;
                   right--;
                }
            }
        }
        
        
        return [...new Set(result.map(x => JSON.stringify(x)))].map(JSON.parse);
    };


## 1550. Three Consecutive Odds

https://leetcode.com/problems/three-consecutive-odds/

#### Breakdown

---

 Di naman tayo makakapag - solve ng problem if less than 3 lang yung
 laman ng array natin haha.

    if(arr.length < 3){
            return false;
        }


---
Gusto lang natin mag loop up to minus 2 kasi yung 2 is occupied by 2 pointers.

       for(let x = 0 ; x < arr.length - 2; x++){


---

If the first number is not odd there's no point na mag continue pa sa 
pag loop kasi di rin tayo makaka form ng 3 consecutive ng odds kung yung unang item palang di na odd.

Else naman nag set ako ng 2 pointers. The first pointer is pointing sa item na kasunod nung current item or yung x tapos yung right pointer naman yung kasunod lang na item nung left pointer.

If kahit isa sa dalawang pointer na yan hindi odd yung mga laman edi no 
point naman na mag continue pa kasi di rin maka form ng 3 odds talaga.


     if(!isOdd(arr[x])){
           continue;
    } else {
           const lp = x + 1;
           const rp = lp + 1;
                    
           if(!isOdd(arr[lp]) || !isOdd(arr[rp])){
                 continue;
            } else {
                 return true;
                    }
     }

---

***Code***

    const isOdd = (number) => number % 2 !== 0;
    
    var threeConsecutiveOdds = function(arr) {
        if(arr.length < 3){
            return false;
        }
    
        
        for(let x = 0 ; x < arr.length - 2; x++){
            if(!isOdd(arr[x])){
                continue;
            } else {
                const lp = x + 1;
                const rp = lp + 1;
                
                if(!isOdd(arr[lp]) || !isOdd(arr[rp])){
                    continue;
                } else {
                    return true;
                }
            }
        }
        
        return false;
    };


## 389. Find the Difference

https://leetcode.com/problems/find-the-difference/


### Breakdown

---

First step pinagsama ko muna yung contents nung dalawang string.
Pagka spread ko naging individual elements or characters na sila papasok sa new array.

Tapos nag map ako every char is ginawa kong charcode or ASCII para maging integer equivalent.

Next step is to reduce every ascii integer or char code nag perform ako ng Bit XOR operator para ma filter out kung ano ba yung unique using bit comparison.

Pagkalabas nung unique element binalik ko ulit sa pagiging string.

    var findTheDifference = function(s, t) {
    
       let res = [...s, ...t].map(letter => letter.charCodeAt(0)).reduce((acc, num) => acc ^ num, 0);
        
        return String.fromCharCode(res)
    };


## Smallest Difference

***Problem***

Given two arrays of equal length gusto natin mahanap yung pair of numbers na galing sa array 1 at array 2 na may smallest difference or malapit sa isa't isa.

***Example:***

Array 1: `[1,10,23,5,44]`
Array 2 : `[5,2,91,3,4]`

The answer would be `[1,2]` kasi ang difference lang nila ay `1`

Now how can we solve it in an efficient way?

### Breakdown

---

The first step is ***i-sort muna yung dalawang arrays pa ascending order.***

    arr1 = arr1.sort((a,b) => a - b);
    arr2 = arr2.sort((a,b) => a - b);

By sorting yung dalawang arrays mas makakapag-compare tayo ng values kung mas malaki ba yung number sa array 1 kumpara sa array 2 or mas maliit ba resulting to a least difference.


---

Need natin mag declare ng dalawang pointers.
Yung first pointer pang traverse sa items sa Array 1 at yung second pointer
pang traverse sa Array 2 items.

resultset variable is diyan mai-store yung pairs na may least difference.

    let pointerx = 0;
    let pointery = 0;
    let resultset = [];
    let smallest = null;
    let difference = null;


---

Dito naman gusto ko mag loop sa Array  at Array 2 using two pointers.
Hindi mag ii-stop yung loop hanggat hindi ko nadadaanan yung lahat ng items sa both arrays.

Sa loob ng loop merong comparison kung mas maliit ba yung rightnumber sa leftnumber.

Kung mas maliit gusto ko i-move yung pointer x pa kanan. Bakit? 
Kasi sorted nga yung array natin gusto ko magkaroon ng larger value to minimize the gap between the two numbers.

Kung mas malaki yung leftnumber, gusto ko naman ma-move yung pointer sa second array. Same thing to minimize the gap.

Third if statement sinasabi diyan kung mas maliit yung nakuhang difference
between leftnumber and rightnumber gusto ko i-assign yung values na yan as
the smallest number na current or parang title holder haha.

If nadaanan na lahat return nalang yung resultset.

        while(pointerx !== array1.length - 1 && pointery !== array2.length - 1){
        	const leftnumber = array1[pointerx];
        	const rightnumber = array2[pointery];
           
           if(leftnumber < rightnumber){
            diff = rightnumber - leftnumber;
            pointerx++;
          } else if (leftnumber > rightnumber) {
              diff = leftnumber - rightnumber;
        	  pointery++;
          } else {
             return [leftnumber, rightnumber];
        }
        
          if(diff < smallest){
        	smallest = diff;
        	resultset = [leftnumber, rightnumber];
         }
        }
        
    return resultset;


## Caesar Cipher

### Breakdown

---

First step brineakdown ko muna yung string into individual letters or chars.
Second, possible kasi na mag input yung user ng large value for the skip or rotation.

***Kung ganito mangyayari pwedeng mag-exceed yung skip sa limit ng ASCII Keycode Alphabet*** so ang ginawa ko is ***nag mod ako gamit 26 (number of letters sa alphabet).***

Para repeatedly magminus ng 26 hanggang makuha yung remainder. Yung remainder bale yung magiging new key.

Tapos nag loop ako every letter and then tinawag ko yung `getNewLetter` na function.


    const  caesarCipher = (string, rotation) => {
	    const  ltrs = [...string];
	    const  newkey = rotation % 26;
	    
	    let  res = [];
	      
	    for(const  letter  of  ltrs){
		    res.push(getNewLetter(letter, newkey))
	    }
	       
	    return  res.join('');
    };

---

***Sa function naman na to ginawa ko is kinuha ko yung ASCII keycode nung letter plus yung skip / rotation na specified.***

If mas mababa sa ASCII Alphabet Keycode limit na 122 or equal edi pasok at kailangan nalang i-return yung new letter.

Pero ***kung mas malaki sa limit need natin i-add yung starting point ng ASCII code alphabet - 1 which is 64 added by new letter code tapos mod 122.***

Kasi ***paano kung z yung letter edi keycode niya is 122 tapos yung key natin is 21. Edi 143 na yung new letter code which nag exceed na sa limit na 122.***

***So need natin ulit mag mod (newlettercode mod endascii) tapos add startascii
kasi need natin magstart sa ASCII Alphabet keycodes.***




    const  getNewLetter = (letter, key) => {
	    const  newlettercode = letter.charCodeAt() + key;
	    const  startascii = 64; 
	    const  endascii = 122;
	    
	    if(newlettercode <= endascii ){
		    return  String.fromCharCode(newlettercode);
	    } else {
		    return  String.fromCharCode(startascii + newlettercode % endascii)
	    }
    }



---



***Code***

    const  getNewLetter = (letter, key) => {
	    const  newlettercode = letter.charCodeAt() + key;
	    const  startascii = 64; 
	    const  endascii = 122;
	    
	    if(newlettercode <= endascii ){
		    return  String.fromCharCode(newlettercode);
	    } else {
		    return  String.fromCharCode(startascii + newlettercode % endascii)
	    }
    }
         
    
    const  caesarCipher = (string, rotation) => {
	    const  ltrs = [...string];
	    const  newkey = rotation % 26;
	    
	    let  res = [];
	      
	    for(const  letter  of  ltrs){
		    res.push(getNewLetter(letter, newkey))
	    }
	       
	    return  res.join('');
    };
    
      
    
    console.log(caesarCipher("zbC", 27));


## 977. Squares of a Sorted Array

https://leetcode.com/problems/squares-of-a-sorted-array/

### Breakdown

---

Dito nag declare ako ng dalawang pointer for the start of the array and then sa pinakadulo ng array.

      let lp = 0;
      let rp = A.length - 1;

---

Right from the bat gusto natin i-compare yung magkabilang dulo ng array natin.
Kaya nilagay ko na agad yung dalawang numbers sa two variables.

     let x = A[lp] * A[lp];
     let y = A[rp] * A[rp];


---

So habang hindi pa nagkakasalubong yung dalawang pointers sa gitna gusto natin
i-compare yung values ng x at y. If mas malaki yung x or nasa left value gusto natin
ipush yung x at imove yung left pointer pa-kanan otherwise vice-versa naman.

        while(lp <= rp){
            if(x > y){
                res.push(x);
                lp++;
                x = A[lp] * A[lp];
            } else {
                res.push(y);
                rp--;
                y = A[rp] * A[rp];
            }
        }

---

***Example simulation:***

	// [-4,-1,0,3,10]
	
    // Step 1
    16 < 100 ? [100]
    // Step 2
    16 < 9 ? [100,16]
    // Step 3
    1 < 9 ? [100,16,9]
    // Step 4
    1 < 0 [100,16,9,1]
    // Step 5
    0 < 0 [100,16,9,1]
    // Step 6
    Break na yung loop kasi nagtagpo na yung dalawang pointers or nag-equal na sila.

---

Since gusto natin na ascending order yung array we want to reverse the array.

    return res.reverse();

***Code***

    /**
     * @param {number[]} A
     * @return {number[]}
     */
    var sortedSquares = function(A) {
        let lp = 0;
        let rp = A.length - 1;
        
        let res = [];
        let x = A[lp] * A[lp];
        let y = A[rp] * A[rp];
        
        while(lp <= rp){
            if(x > y){
                res.push(x);
                lp++;
                x = A[lp] * A[lp];
            } else {
                res.push(y);
                rp--;
                y = A[rp] * A[rp];
            }
        }
        return res.reverse();
    };

