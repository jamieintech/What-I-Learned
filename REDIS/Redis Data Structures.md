# Redis Data Structures



## Keys

- Unique
- Binary safe 
  - any binary sequence can be used as a key
- Key names can be up to 512MB
  - But long key names are not recommended
- Length VS Readability
- case sensitive
  - registeredusers != RegisteredUsers



### Key Spaces

- Within a logical database, a single flat key space exists

  - all key names occupy the same space

- No automatic separation of key names

- Need to consider naming convention

  - the goal of redis is to keep things simple
  - therefore, complex key names should be avoided



### Logical Databases

- the default is database 0 (zero-based index)
- same key name can appear in multiple logical databases
  - it's best to separate key spaces for a single application rather than separating multiple applications



### Example

- `user:1000:followers`
  - `user`: object name
  - `1000`: unique identifier or the insatnce
  - `followers`: composed object
  
  

