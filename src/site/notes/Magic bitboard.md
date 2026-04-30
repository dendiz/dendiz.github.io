---
{"dg-publish":true,"permalink":"/magic-bitboard/","dg-note-properties":{}}
---


I have talked about representing a chess board as a series of bits (and thus an 64 bit int) in [[Chess Bitboard\|Chess Bitboard]]. Now  
let's take it one step further to optimize sliding move generation using pre computed tables of bitboards.  

The idea is the following:  
Iterating over each possible bit and direction for a sliding piece like a bishop/rook takes a while. You need to manage indices and probe the correct places in the bitboard. What if we could pre-compute all the possible movements and save them in a lookup table? How many possible combos are there? Well let's think of a rook... It can be on any one of the  
64 squares. On each square it will have a bunch of squares that it can attack, let's assume it's on A1  
  
```  
1 . . . . . . .  
1 . . . . . . .  
1 . . . . . . .  
1 . . . . . . .  
1 . . . . . . .  
1 . . . . . . .  
1 . . . . . . .  
X 1 1 1 1 1 1 1  
```  
  
It looks like there are 14 squares it can attack from there. But if we think a bit more, we don't really need to think include the edges of the board because it cannot be blocked by a case we have not yet already considered when getting the to edges. This will become clearer as we put blocking pieces in the path.  
  
```  
. . . . . . . .  
1 . . . . . . .  
1 . . . . . . .  
1 . . . . . . .  
1 . . . . . . .  
1 . . . . . . .  
1 . . . . . . .  
X 1 1 1 Y . . .  
```  
Now if there is a blocking piece Y in the path the number of squares reduces to 10. So each of these reachable squares can be represented by a bit in the bit board. Now if the Rook is on a corner it needs 12 bits to address all the squares it can attack. If it's on the edge it needs 11 bits, if it's in the interior it needs 10 bits. Each of these bits can be flipped to indicate a blocker. So:  
- 4 corners = 4 x 2^12  
- 4 x 6 edges = 24 x 2^11  
- 36 interior squares = 36 x 2^10  

there are around 100K unique items which is storable. The problem is how do we index these into the array. The input to our function is a bitboard that is 64 bits. If we were to index by this input our key space would be 2^64 which is not maintainable. We need something that squeezes that 2^64 key space into the 100K array. Here's s simplified example:  
  
you have 3 players with jersey numbers:
- 17  
- 47  
- 57  

that you want to map. So jersey number → player instance. If you were to index by jersey number, you would need an array of size 100 (00 to 99) but only 3 slots would be populated. Wasteful in this case, in the chess case impossible (2^64 slots). So you need a hashing algorithm, which is what magic bitboards provide. Say you were to multiple each jersey number with 6 and take the 100s digit.  
  
- 17*6 = 102  
- 47*6 = 282  
- 57*6 = 342  

now you can store these in an array of size 3, and you magic number is 6. This is exactly what is happening. So in essence we have 12 bits for our rook, that can be 0 or 1 which we want to compress into the top 12 bits of our 64 bit int. And we need a magic number to multiply with that will push these to the upper 12 bits and then we will shift these by 64 - 12 = 52 bits right to place them in the lower half and that will be our index in the lookup array. 

The algorithm can be summarized as follows (applied for each square, for bishop and rook separately)
1. generate a mask that casts rays from the source square into the possible directions for the piece (not covering the edge squares)
2. generate bitboards with all subsets of the set bits from step 1
3. Generate a sliding attack bitboard using looping techniques for each of the bitboards obtained from step 2
4. generate a sparse 64 bits random number (sparse mean bitwise and 3 64bit ints) as they seem to provide faster results
5. use this generated magic to map the sliding attack to a table. If there is an existing entry for that index, discard the random number and try again
6. if you can map all the sliding attacks without collision that random is the magic number for that piece on that square.


- 