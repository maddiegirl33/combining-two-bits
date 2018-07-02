def two_bits(matrix1, matrix2):

    # dimension size of matrixes and seeing which nodes to connect
    matrix1 = np.array(matrix1)
    matrix2 = np.array(matrix2)
    dim = int(sqrt(np.size(matrix2))) - 1
    dim2 = int(sqrt(np.size(matrix1)))
    n1 = int(input("Matrix 1 - 1st bit: "))
    n2 = int(input("Matrix 1 - 2nd bit: "))
    n3 = int(input("Matrix 2 - 1st bit: "))
    n4 = int(input("Matrix 2 - 2nd bit: "))
    
    # expanding the first matrix to new dimensions and adding element
    matrix1 = np.pad(matrix1, ((0,dim-1), (0, dim-1)), mode = 'constant', constant_values=0)
    matrix1[n1-1][n1-1] += matrix2[n3-1][n3-1]
    matrix1[n2-1][n2-1] += matrix2[n4-1][n4-1]

    # deletes the Jii element and saves col & row
    row = np.delete(matrix2[n3-1:n3, :dim+1], n3-1)
    row2 = np.delete(matrix2[n4-1:n4, :dim+1], n3-1)
    col = np.delete(matrix2[:dim+1, n3-1:n3], n3-1)
    col2 = np.delete(matrix2[:dim+1, n4-1:n4], n3-1)
    
    # adding the RIGHT weights, hopefully
    matrix1[n1-1][n2-1] += matrix2[n3-1][n4-1]
    matrix1[n2-1][n1-1] += matrix2[n4-1][n3-1]
    
    # deleting the added element
    row = np.delete(row, n4-2)
    col = np.delete(col, n4-2)
    row2 = np.delete(row2, n3-2)
    col2 = np.delete(col2, n3-2)      
    
    # deleting the columns 
    matrix2 = np.delete(np.delete(matrix2, (n3-1, n4-1), axis=0), (n3-1, n4-1), axis=1)

    # filling in rows and columns
    for i in range(len(row)):
        matrix1[n1-1][dim2+i] = row[i]
        matrix1[n2-1][dim2+i] = row2[i]
        matrix1[dim2+i][n1-1] = col[i]
        matrix1[dim2+i][n2-1] = col2[i]

    for i in range(dim-1):
        for j in range(dim-1):
            matrix1[dim2+i][dim2+j] = matrix2[i][j]
        
    return matrix1 
