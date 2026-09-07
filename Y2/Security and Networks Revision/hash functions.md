#SaN 

A **hash function** is any function that can be used to map **data** of abritrary size to fixed-size values, though there are some hash functions that support variable-length.   
A hash function may be considered to perform three functions:  

- Convert variable-length keys into fixed-length values
- Scramble the bits of the key so that the resulting values are uniformly distributed over the keyspace
- Map the key values into ones less than or equal to the size of the table.

It should satisfy two properties:

- Be very fast to computer
- Minimise duplication of output values (**collisions**)

Hash functions rely on generating **probability distributions** for their effectiveness, reducing access time to nearly constant.