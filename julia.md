# Julia

* Sparse matrix

  We should avoid the `.` operation with sparse matrix:
  
  ```
  using SparseArrays
  using Random
  
  M = 10
  A = rand(M,M)
  B = sparse([1], [2], [0.2], M, M)
  
  #Dot add
  @. A += B
  
  #Add
  A += B
  ```
  
  These operation will treat `B` as a densy matrix, the better way should be
  
  ```
  Nlg = nnz(B)
  Iv, Jv, Vv = findnz(B)
  for k in 1:Nlg
      A[ Iv[k], Jv[k] ] += B[k]
  end
  ```
