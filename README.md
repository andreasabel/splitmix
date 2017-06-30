# splitmix

Pure Haskell implementation of SplitMix pseudo-random number generator.

## dieharder

> [Dieharder](http://webhome.phy.duke.edu/~rgb/General/dieharder.php) is a random
number generator (rng) testing suite. It is intended to test generators, not
files of possibly random numbers as the latter is a fallacious view of what it
means to be random. Is the number 7 random? If it is generated by a random
process, it might be. If it is made up to serve the purpose of some argument
(like this one) it is not. Perfect random number generators produce "unlikely"
sequences of random numbers &ndash; at exactly the right average rate. Testing a rng
is therefore quite subtle.

```
time dieharder-input splitmix | dieharder -a -g 200
```

The test-suite takes around half-an-hour to complete.
All tests are PASSED (occasionally WEAK).

In comparison, built-in [Marsenne Twister](https://en.wikipedia.org/wiki/Mersenne_Twister)
test takes around 15min.

```
time dieharder-input -a
```

## benchmarks

```
benchmarking list/random
time                 96.77 μs   (96.28 μs .. 97.35 μs)
                     1.000 R²   (1.000 R² .. 1.000 R²)
mean                 96.77 μs   (96.35 μs .. 97.63 μs)
std dev              2.001 μs   (1.028 μs .. 3.796 μs)
variance introduced by outliers: 15% (moderately inflated)

benchmarking list/tf-random
time                 60.43 μs   (60.12 μs .. 60.79 μs)
                     1.000 R²   (1.000 R² .. 1.000 R²)
mean                 60.52 μs   (60.26 μs .. 60.91 μs)
std dev              1.120 μs   (780.2 ns .. 1.513 μs)
variance introduced by outliers: 14% (moderately inflated)

benchmarking list/splitmix
time                 16.38 μs   (16.29 μs .. 16.47 μs)
                     1.000 R²   (0.999 R² .. 1.000 R²)
mean                 16.34 μs   (16.25 μs .. 16.51 μs)
std dev              386.8 ns   (201.5 ns .. 669.8 ns)
variance introduced by outliers: 24% (moderately inflated)

benchmarking tree/random
time                 115.4 μs   (108.6 μs .. 126.0 μs)
                     0.942 R²   (0.910 R² .. 0.977 R²)
mean                 116.0 μs   (110.3 μs .. 124.2 μs)
std dev              23.47 μs   (16.60 μs .. 33.95 μs)
variance introduced by outliers: 95% (severely inflated)

benchmarking tree/tf-random
time                 132.4 μs   (132.2 μs .. 132.5 μs)
                     1.000 R²   (1.000 R² .. 1.000 R²)
mean                 132.5 μs   (132.3 μs .. 132.6 μs)
std dev              403.3 ns   (323.0 ns .. 516.5 ns)

benchmarking tree/splitmix
time                 59.80 μs   (59.42 μs .. 60.15 μs)
                     1.000 R²   (0.999 R² .. 1.000 R²)
mean                 59.61 μs   (59.26 μs .. 60.36 μs)
std dev              1.683 μs   (864.5 ns .. 3.206 μs)
variance introduced by outliers: 27% (moderately inflated)
```

Note: the performance can be potentially further improved when GHC gets
[SIMD Support](https://ghc.haskell.org/trac/ghc/wiki/SIMD/Implementation/Status).
