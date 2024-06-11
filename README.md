# Matrix_transpose_using_GPU
Performing matrix transpose using GPU with different methods and comparing performance. First, transpose is performed with each thread performing transpose of one element of matrix and later the unrolling option is also implemented. 

Following is the description of the different kernels within the code:

# transpose_read_row_write_column()
In the above kernel for matrix transpose, matrix memory reads are row major, hence coalesced memory access. Each row from the original matrix is stored in columns of transpose matrix, so memory writes are uncoalesced memory writes. Each thread performs transpose for one element of matrix.

# transpose_read_column_write_row()
In the above kernel for matrix transpose, matrix memory reads are column major, hence uncoalesced memory access. Each column from the original matrix is stored in rows of transpose matrix, so memory writes are coalesced memory writes. Each thread performs transpose for one element of matrix.

# copy_row()
This kernel copies the matrix in row major format. So both the read and write operation are coaleaced operations. This gives and idea of maximum performance we can achieve for transpose operation.

# copy_column()
Copies the matrix in column major format. So both the read and write operation are uncoaleaced. This gives lower bound of the memory performance.

Using nvprof, we can print the Global Memory Load Efficiency and Global Memory Store Efficiency for the above functions. For the transpose_read_row_write_column() kernel, the Global Memory Load Efficiency is 100%, whereas the Global Memory Store Efficiency is 12.5%. We get reverse values for transpose_read_column_write_row() kernel.


# transpose_unroll4_row()
In this kernel, the unrolling has been performed using 4 as the unrolling factor. Row major unrolling has been performed here.

# tranpose_diagonal_row()
This kernel avoids partition camping in the DRAM by allowing consecutive thread blocks to access non-consecutive data blocks using the diagonal coordinate system. Within a single thread block, threads still access consecutive memory addresses to adhere the coalesced memory access. 

The above different kernels can be run by using appropriate argument while running the code.


