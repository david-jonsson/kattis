# noll-tv-er
My solution to Núll og tveir, which wont get accepted since it works on integers. Since this problem deals with number up to 10^50 we need to work with strings or big ints (which there are none of in c++) to solve the whole set of problems. But I didnt realise that until I already implemented the algorithm. Anyway, I liked my solution so I will post it here:

```c++
#include <iostream>
#include <cmath>
#include <cassert>

constexpr uint64_t rec(uint64_t n) {
    switch (n)
    {
        case 2u: return 2;
        case 1u:
        case 0u: return 1;
        default:
            uint64_t
                log2    = std::log10(n/2),
                log3    = std::log10(n/3),
                done    = (log3 == log2),
                combs   = std::pow(2, (log2 + (done ? 1 : 0))),
                rest    = n % (uint64_t)(2 * std::pow(10, log2));
            return combs + (done ? 0 : rec(rest));
    }    
}

static_assert(rec(123456) == 32);
static_assert(rec(221) == 7);
static_assert(rec(10) == 2);
static_assert(rec(222) == 8);
static_assert(rec(300) == 8);
static_assert(rec(20000000000000000) == 65537);
static_assert(rec(30000000000000000) == 131072);

int main() {
    std::string line;
    while (std::getline(std::cin, line))
    {
        uint64_t n{};
        try 
        {
            n = std::stoll(line);
            std::cout << rec(n) << std::endl;
        }
        catch (std::out_of_range &e) 
        { 
            std::cout << "Integer overflow\n"; 
            continue;
        }
    }
    return 0;
}
```
