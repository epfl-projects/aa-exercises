## Problem 1

We first show that the OPT strategy is as follows:

- rent [if T < N]
- buy cheap skis [if 2N => T >= N]
- buy cheap skis and rent T - 2N times [if 3N > T > 2N]
- buy expensive skis [if T >= 3N]

The reasons are given below:

(1) T < N. In this case, rent costs less than N, while the other two choices will cost at least N.

(2) N =< T <= 2N. In this case, buy cheap skis costs N, while the other two choices will cost more than N.

(3) 2N < T < 3N. In this case, buy cheap skis and rent T-2N times will cost less than 2N, while other two choices will cost at least 2N.

(4) T >= 3N. In this case, buy expensive costs 2N, while no combination of the other two choices would cost less than 2N.

The strategy for an online algorithm is as follows:

- rent skis [when i < N]
- buy cheap skis [when i = N]
- use cheap skis [when N < i < 3N]
- buy expensive skis [when i = 3N]
- use expensive skis [when i > 3N]

We compare the performance analysis below:

(1) T < N. Cost(OPT) = Cost(strategy) = T. Ratio = 1.

(2) N =< T < =2N. Cost(OPT) = N. Cost(strategy) = N + N = 2N. Ratio = 2.

(3) 2N < T < 3N. Cost(OPT) = N + T - 2N = T - N < 2N & > N. Cost(strategy) = N + N = 2N. Ratio is between [1, 2].

(4) T >= 3N. Cost(OPT) = 2N. Cost(strategy) = N + N + 2N = 4N. Ratio is 2.

So our strategy is at most 2 times worse than the optimal strategy.

cost

      ^
      |
      |
4N    |             ***************
      |             *
      |             *
2N    |  ************ ______________
      |  *           /
      |  *          /
N     |  * ________/
      |  */
      | */
      |*/---------------------------> k
          N      2N  3N

       Figure 1. OPT VS. Strategy

Question:

- How to prove this is the best online strategy?
- In real world, people don't care about money but the actual amount of difference.
- In real world, un-used equipments can be sold.

## Problem 2

## Problem 3

### 3.1

The strategy is as follows:

1. The dog search the right for a randomly chosen distance d.
2. If not found, then search the other direction doubling the distance
3. repeat the step above until the bone is found.

If the bone is found after k steps, we must have 2^k * d >= x and x > 2^(k - 2) * d. The total cost of searching is as following:

Cost = 2*d + 2*2d + 2*2^2*d + ... 2*2^i*d + ... + x
     <=  2*d + 2*2d + 2*2^2*d + ... 2*2^i*d + ... + 2*2^k*d
     = 2d * (1 + 2 + 2^2 + ... + 2^k)
     = 2d * (2^(k + 1) - 1)
     < 2d * (8x/d - 1)
     = 16x - 2d

Now suppose in each step, instead of doubling the distance, we multiply the distance by m. m^k * d >= x and x > m^(k - 2)*d. Then we have:

Cost = 2*d + 2*md + 2*m^2*d + ... + 2*m^i*d + ... + x
     <= 2*d + 2*md + 2*m^2*d + ... + 2*m^i*d + ... + 2*m^k*d
     = 2d * (1 + m + m^2 + ... + m^k)
     = 2d * (m^(k + 1) - 1)/(m - 1)
     = 2d*(m^3*x/d - 1)/(m - 1)
     = (2*m^3*x - 2d)/(m - 1)
     = 2*m^3/(m-1) * x - 2d/(m-1)

The function f(m) = 2*m^3/(m - 1). m = 2 is not the smallest ratio. There exists a mimimum 1.5. If m = 1.5, ratio = 13.5.

What if Fibonacci run times? Following is Fibonacci approach:

1. The dog searches the right for a randomly chosen distance d.
2. If not found, then search the left for d.
3. If not found, then search the other direction with the distance as the sum of two previous searches.
4. repeat the step above until the bone is found.

If we denote the fibonacci series as follows:

f(1) = f(2) = 1, f(n) = f(n - 1) + f(n - 2)

If the bone is found after k steps, we must have d*f(k) >= x and x > d*f(k - 2). The total cost of searching can be calculated as follows:

Cost = 2*f(1)*d + 2*f(2)*d + ... + 2*f(i)*d + ... x
     <= 2*f(1)*d + 2*f(2)*d + ... + 2*f(i)*d + ... 2*f(k)*d
     = 2d* (f(1) + f(2) + ... + f(k))
     = 2d * (f(k + 2) - 1)

     f(k + 2) = f(k + 1) + f(k) = 2*f(k) + f(k - 1) = 3*f(k - 1) + 2*f(k-2) = 3*f(k-3) + 5*f(k-2) < 8*f(k-2)

     < 2d * (8*f(k-2) -1)
     < 2d * (8x/d - 1)
     = 16x - 2d


### 3.2

The algorithm is as follows:

1. The dog search all direction with distance d.
2. If not found, then search all direction by multiplying the distance by a.
3. repeat the above step until the bone is found.

If the bone is found in after k rounds, we must have d*a^k >= x and x > d*a^(k - 1). Then the total cost of searching is as follows:

Cost = m*2*a^0*d + m*2*a^1*d + ... + m*2*a^i*d + ... + Cost_last_round
     <= m*2*d + m*2*a*d + ... + m*2*a^i*d + ... + m*2*a^k*d
     = m*2d(1 + a + ... + a^k)
     = m*2d(a^(k+1) - 1)/(a - 1)
     < m*2d(a^2*x/d -1)/(a - 1)
     < 2m * a^2/(a-1)

let a = 2, then Cost < 8m = O(mx).

Then, we must also prove that Cost = Ω(mx).
