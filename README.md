[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/OlW38W4k)
# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.

The recursion stops when $n \le 1$. As the mystery function is called, it recursively calls 
itself 3 times each time dividing n by 3. This results in the mystery function part of the 
runtime to be 3T(n/3).
There is also a loop which runs n^5 times based on the loop conditions.

Therefore our recurrence relation looks something like:

T(n) = 3T(n/3) + n^5 + some constants which dont matter
    
   = 3(3T(n/9) + (n/3)^5) + n^5 = 9T(n/9) + n^5/3^4 + n^5
         
   = 9(3T(n/27) + (n/9)^5) + (n^5/3^4) + n^5 = 27T(n/27) + n^5/9^4 + n^5/3^4 + n^5
         
 ...
 
   = 3^iT(n/3^i) + n^5 $\sum_{k=0}^i 1 \ over (3^(4(k-1)))$
         
So take: i = log(n) which simplifies the expression to:
    
   = n + n^5 so take the bigget term: O(n^5)

So $T(n) \in O(n^5)$

