*HU, HUIYU*

### Overall Grade: 77/100

### Quality of report: 10/10

* Is the homework submitted (git tag time) before deadline? 

	Yes. `2018-05-11 23:57:43 -0700`. 

* Is the final report in a human readable format html?  

	Yes,  `html`.

* Is the report prepared as a dynamic document (Jupyter notebook) for better reproducibility?

	Yes, `ipynb`.

* Is the report clear (whole sentences, typos, grammar)? Do readers have a clear idea what's going on and how are results produced by just reading the report?

	Clear report.
 
### Correctness and efficiency of solution: 31/50 

* Q1 (16/25 pts)

    1, 3) (8/15 pts)
    
    **Efficiency(8/11pts)**
    Dr. Zhou's implementation for `r = 20` has memory estimate 7.12 MB and allocs estimate 10, while yours is `1.30 k allocations: 4.209 GiB, 6.18% gc time`. There is a lot of room for improving efficiency.
    - Use pre-allocation to save gabbage collection: Dr. Zhou's implement uses half of the memory in pre-allocation. For more details, please check Dr. Zhou's implement (-1 pt)
    - The update of matrix `V` can be formulated as `V = V .* (XW^T) ./ (VWW^T)`. Notice here the dimension of matrix `V` and `W` are `(m, r)` and `(r, n)`, respectively, and `r \ll n or m`. When calculating `VWW^T`, one should calculate `V(WW^T)` instead of `(VW)W^T`, which can reduce the required flops from `4mnr` into `2nr^2 + 2mr^2 = 2(m + n)r^2` (-2 pts)

     **Correctness(0/4 pts)**
     The code fails to generate the correct answer in part 6. And I cannot reproduce your code on my computer to check the correctness  
      
     **Others**
    - Using `vecnorm` instead of `sum(abs2, X - A_mul_B!(mul_VW, V, W))` will speed up your function
    
    4, 5) (4/5pts) This question is not a convex question, so there is no guarantee for unique result with random initial input matrix. 
    2, 6) (4/5pts) Since your function fail to give the correct output, your conclusion in part 6 is wrong. 


* Q2 (15/25 pts)

    1) (5/5pts) 
    2) (20/20 pts)
    **Algorithm(0/7pts)**
    - Use Woodbury formula to reduce the computational power and storage requirement (-4 pts)
    - Use Cholesky decompostion instead of taking inverse in the calculation of likelihood (-3 pts)
    
    **Efficiency(4/7pts)**
    Dr. Zhou's implementation has memory allocation 1.34KB, yours is 153.93KB. Some suggestions:
    - chunk 9: The determinant should be computed after the Cholesky decomposition. One can speed up the function `logdet()` by putting a Cholesky decomposition in `logdet()`. (-1 pt)
    - The extra memory allocation caused by transpose can be avoid by using Blas functions in `y' * inv(Σ)`(-1 pts)
    - Use `BLAS.syrk!()` to reduce memory allocation in `σ1^2 * Z * Z' + σ0^2 * I` and save all symmetric matrix in form symmetric (-1 pts)
   
   **Correctness(6/6pts)**

    **Others**
    You can check the input to make the function more stable for wrong input.
    
### Usage of Git: 10/10

* Are branches (`master` and `develop`) correctly set up? Is the hw submission put into the `master` branch?

	Yes.

* Are there enough commits? Are commit messages clear? 

	Yes

* Is the hw2 submission tagged? 

	Yes

* Are the folders (`hw1`, `hw2`, ...) created correctly?

	Yes.	

* Do not put a lot auxillary files into version control.  

	Yes.
		

### Reproducibility: 8/10

* Are the materials (files and instructions) submitted to the `master` branch sufficient for reproducing all the results? (-2 pts)

	A lot of results cannot be reproduce, eg Chunk 5, no definition of `X` before using it. Chunk 12, I cannot run the chunk

* If necessary, are there clear instructions, either in report or in a separate file, how to reproduce the results?  

	Not applicable for hw2.

### Julia code style: 18/20

* Rule (4): 4 spaces for indenting.

* Rule (6): Never place more than 80 characters on a line.

* Rule (7): Always include a single space after a comma. 

* Rule (8):  Never insert a space before a comma.

* Rule (9): Always insert a single space before and after an operator, except for the `^` and `:` operators, which never have spaces around them. (-2 pt)

    - code chunk 9 middle, `@inbounds V[i, j] = V[i, j]*(num_V[i, j] / den_V[i, j])` 
    - code chunk 9 bottem, `if  abs(loss - lastloss)/(abs(lastloss) + 1.0) < tol`

* Rule (12): When naming variables or functions, use short lowercase names if possible.

* Rule (13): If a variable or function name is too long to be read in all lowercase, insert underscores at word boundaries.

* Rule (16): When naming constants, use all caps.
