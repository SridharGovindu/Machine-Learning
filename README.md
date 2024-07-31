import pandas as pd
import numpy as np
#read data from excel
xls = pd.read_excel("Lab_Session_Data.xlsx")
xls
#drops nan columns
data = xls.dropna(how= "any", axis=1)
#drops row customer to make sure that we don't get duplicate indices
data.drop(["Customer"], axis = 1, inplace = True)
A = data.iloc[:, :-1].to_numpy() #feature vectors
C = data.iloc[:, -1].to_numpy() #target vectors
C = C.reshape(-1,1)
print("Dimensionality of matrix A:", A.shape) #dimensions of A matrix
print("No. of vectors in vector space ",A.shape[0]) #no. of vectors
print(A)
print(C)
l = len(C) #length of matrix
k = 0
#Rich and poor verification of customers
for i in range(l):
    if C[i] > 200:
        print("Customer no. C",k,"is rich")
        k = k + 1
    else:
        print("Customer no. C",k,"is poor")
        k = k + 1
#matrix A inverse
D = np.linalg.pinv(A)
result = np.dot(D, C)
#resultant vector
print("The X vector is: ")
print(result)
rank = np.linalg.matrix_rank(A)
print("Rank of the given Matrix is : ",rank) #rank of matrix
