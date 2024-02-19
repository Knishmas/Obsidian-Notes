## Binary search 
- Trick to calculating *midpoint* . You do this to prevent overflow (edge case) 
- **Middle = left +(right-left) / 2**            *Prevents overflow*
- Rather than:  middle = right - left / 2            *DOESN'T prevent overflow*
- Prevents integer overflow 