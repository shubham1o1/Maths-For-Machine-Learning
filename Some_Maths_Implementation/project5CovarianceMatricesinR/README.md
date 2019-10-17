# Covariance Matrices in R in two ways:
---

- Create column vectors and create matrix from vectors

    ```r 

        # Create column vectors
        a <- c(1,2,3,4,5,6)
        b <- c(1,3,5,7,9,11)
        c <- c(10, 20, 30, 40, 50, 60)
        d <- c(2, 5, 5, 2, 1, 0)
        e <- c(4, 5, 6, 7, 8, 9)
        
        # Create matrix from vectors
        M <- cbind(a, b, c, d, e)
        k <- ncol(M) # no. of columns of m
        n <- nrow(M) # no. of rows of m
        
        print(M)

    ```

- Output:

    ```bash
            a  b  c d e
        [1,] 1  1 10 2 4
        [2,] 2  3 20 5 5
        [3,] 3  5 30 5 6
        [4,] 4  7 40 2 7
        [5,] 5  9 50 1 8
        [6,] 6 11 60 0 9
    ```

- Find mean i.e. expectation for each columns

    ```r
        # Find the mean for each column
        # %*% means matrix multiplication
        # Mean means expectation
        k_mean <- matrix(data = 1, nrow = n) %*% cbind(
            mean(a), mean(b), mean(c), mean(d), mean(e))
        print(k_mean)
    ```

- Output:

    ```bash

            [,1] [,2] [,3] [,4] [,5]
        [1,]  3.5    6   35  2.5  6.5
        [2,]  3.5    6   35  2.5  6.5
        [3,]  3.5    6   35  2.5  6.5
        [4,]  3.5    6   35  2.5  6.5
        [5,]  3.5    6   35  2.5  6.5
        [6,]  3.5    6   35  2.5  6.5
    ```

- Find the difference using a difference matrix:

    ```r
        # Create a difference matrix
        diffM <- M - k_mean
        print(diffM)
    ```

- Output:

    ```bash
                a  b   c    d    e
        [1,] -2.5 -5 -25 -0.5 -2.5
        [2,] -1.5 -3 -15  2.5 -1.5
        [3,] -0.5 -1  -5  2.5 -0.5
        [4,]  0.5  1   5 -0.5  0.5
        [5,]  1.5  3  15 -1.5  1.5
        [6,]  2.5  5  25 -2.5  2.5
    ```

- Finally we have all the information required to create a covariance matrix

    ```r
        # Create the covariance matrix
        # t(diffM) calculates the transppose of diffM
        covarM <- (n-1)^-1 * t(diffM) %*% diffM #sample covariance
        print(covarM)
    ```

- Output:

    ```bash
            a  b   c     d    e
        a  3.5  7  35  -2.5  3.5
        b  7.0 14  70  -5.0  7.0
        c 35.0 70 350 -25.0 35.0
        d -2.5 -5 -25   4.3 -2.5
        e  3.5  7  35  -2.5  3.5
    ```

- Diagonal of a covariance matrix is the variance.

    ```r
        # Find variances from the covariance matrix
        variance <- diag(covarM)
        print(variance)
    ```

- Output:

    ```bash
            a     b     c     d     e 
        3.5  14.0 350.0   4.3   3.5 
    ```

- 2nd way is to use the built-in function of R:

    ```r
        > # Use R's built-in functions
        > print(cov(M))
    ```

- Output:

    ```bash
            a  b   c     d    e
        a  3.5  7  35  -2.5  3.5
        b  7.0 14  70  -5.0  7.0
        c 35.0 70 350 -25.0 35.0
        d -2.5 -5 -25   4.3 -2.5
        e  3.5  7  35  -2.5  3.5

    ```