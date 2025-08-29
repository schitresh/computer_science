# Error Detection
- Error is a condition when receiver's information does not match sender's information
- During transmission
  - Digital signals suffer from noise that can introduce errors in the binary bits
  - That means 0 bit may change to 1 bit or vice versa
- To prevent such errors, error detection codes are added as extra data to digital messages

## Types of Errors
- Single Bit Error
  - One bit of a transmitted data is altered during transmission
  - 10-1-1... -> 10-0-1...
- Multi Bit Error
  - Relatively rare than single bit error
  - But can occur in high noise or high interference digital environments
  - 1-0-111... -> 1-1-11-0-...
- Burst Error
  - When several consecutive bits are flipped mistakenly in digital transmission
  - 1-011-1... -> 1-100-1...

## Error Detection Methods
### Single Parity Check
- An extra bit is added to a data transmission
  - 1 is added if it contains odd number of 1's
  - 0 is added if it contains even number of 1's
  - 100011 -> 100011-1
- Cannot detect even number of bit errors
  - That is, if two 1's or two 0's are flipped

### Two-dimensional Parity Check
- Parity check bits are calculated for each row and each column
  - 1100-0 (parity bit for row)
  - 1101-1 (parity bit for row)
  - ....
  - 0001 (parity bits for columns)

### Checksum
- Data is divided into equally sized segments
- Sum of each segment is calculated using a 1's complement
- The calculated sum is sent to the receiver along with the data
- Won't work if one or more bits of a segment are damaged
  - And the corresponding bit(s) of opposite value in second segment are also damaged

## Cyclic Redundancy Check
- Based on binary division unlike checksum which is based on addition
- Sequence of redundant bits are appended to the end of the data unit
  - So that the resulting data unit becomes exactly divisible
  - By a second predetermined binary number
- It is accepted at the destination
  - If there is no remainder on dividing by the same number
