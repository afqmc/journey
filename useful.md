# HDF5

* Show file content in a HDF5 file
  
  ``` 
  h5dump -n twoBody.h5 
  ```

  We will see

  ```
  HDF5 "twoBody.h5" {
  FILE_CONTENTS {
  group      /
   group      /tb
   dataset    /tb/N
   dataset    /tb/i
   dataset    /tb/j
   dataset    /tb/k
   dataset    /tb/l
   dataset    /tb/v
   }
  }
  ```
  
* Show on dataset content in a HDF5 file

  ```
  h5dump -d /tb/N twoBody.h5
  ```
  
  We will see
  
  ```
  HDF5 "twoBody.h5" {
  DATASET "/tb/N" {
   DATATYPE  H5T_STD_I64LE
   DATASPACE  SCALAR
   DATA {
   (0): 8
    }
  }
  }
  ```