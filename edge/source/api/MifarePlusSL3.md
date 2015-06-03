#MifarePlusSL3

Provides access to Mifare Plus tag in security level 3 and I/O operations on an IsoDep Tag object.



##Constructors

**MifarePlusSL3**



##Public Methods

### enable

**public void enable( tag)**

Enable I/O operations to the tag from  IsoDep object and SAM communication.
 May cause RF activity and may block. Must not be called from the main application thread.
 A blocked call will be canceled with MiFarePlusException by calling close() from another thread.
 Only one TagTechnology object can be connected to a Tag at a time.
 Applications must call close() when I/O operations are complete.

**Parameters:**

tag - Contactless tag already detected by device. We get this through the EXTRA_TAG information from the intent.

**Returns:**

void

**Throws:**

com.symbol.emdk.securenfc.MifarePlusSL3Exception



### disable

**public void disable()**

Disables I/O operations to the tag from IsoDep object, closes connection to SAM, and releases resources.
 Also causes all blocked I/O operations on other thread to be canceled and return with MiFarePlusException.

**Returns:**

void

**Throws:**

com.symbol.emdk.securenfc.MifarePlusSL3Exception



### firstAuthentication

**public byte firstAuthentication( keyBlockNo, SamKey samkey,  samDiverseParams,  pcdCap2)**

Performs First authentication on specified block number using SAM key.

**Parameters:**

keyBlockNo - Key Block Number of the block to be authenticated.(range 0x4000 to 0x404F depending card size).
 keyBlockNo represent a key in the card which is the same key that SamKey represent in the SAM.

samkey - SAM key to be used for authentication. Only AES key should be used.

samDiverseParams - Diversification parameters for current key. If present

pcdCap2 - Capabilities of PCD. If present

**Returns:**

byte

**Throws:**

com.symbol.emdk.securenfc.MifarePlusSL3Exception



### followingAuthentication

**public void followingAuthentication( keyBlockNo, SamKey samkey,  samDiverseParams)**

Performs Following authentication on specified block number using SAM key.
 This authentication should be performed after successful First authentication.

**Parameters:**

keyBlockNo - Key Block Number of the block to be authenticated.(range 0x4000 to 0x404F depending card size) .
 keyBlockNo represent a key in the card which is the same key that SamKey represent in the SAM.

samkey - SAM key to be used for authentication. Only AES key should be used.

samDiverseParams - Diversification parameters for current key. If present

**Returns:**

void

**Throws:**

com.symbol.emdk.securenfc.MifarePlusSL3Exception



### resetAuthentication

**public void resetAuthentication()**

Resets authentication status of card.
 After execution of this method, card will be in not authenticated state.
 Hence host must authenticate card before further communication.

**Returns:**

void

**Throws:**

com.symbol.emdk.securenfc.MifarePlusSL3Exception



### readBlock

**public byte readBlock( isEncrypted,  macOnCmd,  macOnResponse,  blockNumber,  numOfBlocks)**

Reads specified number of blocks starting from specified block number.

**Parameters:**

isEncrypted - false: Communication between device and card will be plain
 true: Communication between device and card will be encrypted

macOnCmd - false: Command sent to card will not be MACed
 	true: Command sent to card will be MACed

macOnResponse - false: Response received from card will not be MACed
 true: Response received from card will be MACed

blockNumber - Card block number from which multiple blocks have to be read. (range 0x00 to 0xFF depending card size)

numOfBlocks - Number of blocks to be read. Maximum of 216 blocks can be read

**Returns:**

byte

**Throws:**

com.symbol.emdk.securenfc.MifarePlusSL3Exception

Note:
 1. The specified blocks must be authenticated before calling the read, otherwise the read will fail.
 2. If specified blocks are located in different sectors and are not authenticated with same key, then also read will fail.
 3. Mifare Plus S tag supports only below values of parameters (as per datasheet):
 		encrypted: false
 		macOnCmd: true
 		macOnResponse: true
 4. Parameter macOnCmd: Value false is not allowed for Mifare Plus X, hence user should pass true.

### writeBlock

**public void writeBlock( encrypted,  macOnResponse,  blockNo,  blockData)**

Writes specified number of blocks starting from specified block number.

**Parameters:**

encrypted - false: Communication between device and card will be plain
 true: Communication between device and card will be encrypted

macOnResponse - false: Response received from card will not be MACed
 true: Response received from card will be MACed

blockNo - Card block number from which multiple blocks have to be written(range 0x00 to 0xFF depending card size)

blockData - Data to be written. Maximum of upto 3 blocks can be written

**Returns:**

void

**Throws:**

com.symbol.emdk.securenfc.MifarePlusSL3Exception

Note:
  1. The specified blocks must be authenticated before calling the write, otherwise the write will fail.
  2. If specified blocks are located in different sectors and are not authenticated with same key, then also write will fail.
  3. Mifare Plus S tag supports only below values of parameters (as per datasheet):
  	encrypted: false
  	macOnCmd: true
  	macOnRsp: true

### isValueBlock

**public boolean isValueBlock( macOnResponse,  blockNumber)**

Validates whether specified block is value block or not.

**Parameters:**

macOnResponse - false: Response received from card will not be MACed
 true: Response received from card will be MACed

blockNumber - Block number to be validated

**Returns:**

boolean

**Throws:**

com.symbol.emdk.securenfc.MifarePlusSL3Exception



### readValue

**public int readValue( encrypted,  macOnCmd,  macOnResponse,  blockNumber)**

Reads value from specified value block.

**Parameters:**

encrypted - false: Communication between device and card will be plain
 true: Communication between device and card will be encrypted

macOnCmd - false: Command sent to card will not be MACed
 	true: Command sent to card will be MACed

macOnResponse - false: Response received from card will not be MACed
 true: Response received from card will be MACed

blockNumber - Card value block number to be read. (range 0x00 to 0xFF depending card size)

**Returns:**

int

**Throws:**

com.symbol.emdk.securenfc.MifarePlusSL3Exception

Note:
 1. If sector of specified value block is not already authenticated then readValue will fail.
 2. If specified block is not value block then readValue will fail.
 3. Mifare Plus S tag supports only these values of parameters (as per datasheet):
 	encrypted: false
 	macOnCmd: true
 	macOnRsp: true

### writeValue

**public void writeValue( encrypted,  macOnResponse,  blockNumber,  value)**

Writes value to a specified value block.

**Parameters:**

encrypted - false: Communication between device and card will be plain
 true: Communication between device and card will be encrypted

macOnResponse - false: Response received from card will not be MACed
 true: Response received from card will be MACed

blockNumber - Card value block number to be written(range 0x00 to 0xFF depending card size)

value - Value to be written

**Returns:**

void

**Throws:**

com.symbol.emdk.securenfc.MifarePlusSL3Exception

Note:
 1. If sector of specified block is not already authenticated then writeValue will fail.
 2. This API will convert data block to value block.
 3. To perform operation on value block such as increment(),incrementTransfer(), decrementTransfer(),decrement(),transfer(),restore(),
 we need to call API writeValue() first.
 4. Mifare Plus S tag supports only these values of parameters (as per datasheet):
 	encrypted: false
 	macOnCmd: true
 	macOnRsp: true

### increment

**public void increment( macOnResponse,  blockNumber,  value)**

Increments contents of given value block by specified value and stores result in transfer buffer.
 Content of specified value block will not be affected, until transfer() is called.

**Parameters:**

macOnResponse - false: Response received from card will not be MACed
 true: Response received from card will be MACed

blockNumber - Card value block to be incremented(range 0x00 to 0xFF depending card size)

value - Value to be incremented

**Returns:**

void

**Throws:**

com.symbol.emdk.securenfc.MifarePlusSL3Exception

Note:
 1. If sector of specified value block is not already authenticated then increment will fail.
 2. If specified block is not value block then increment will fail.

### decrement

**public void decrement( macOnResponse,  blockNumber,  value)**

Decrements contents of given value block by specified value and stores result in transfer buffer.
 Content of specified value block will not be affected, until transfer() is called.

**Parameters:**

macOnResponse - false: Response received from card will not be MACed
 true: Response received from card will be MACed

blockNumber - Card value block to be decremented(range 0x00 to 0xFF depending card size)

value - Value to be decremented

**Returns:**

void

**Throws:**

com.symbol.emdk.securenfc.MifarePlusSL3Exception

Note:
 1. If sector of specified value block is not already authenticated then decrement will fail.
 2. If specified block is not value block then decrement will fail.

### restore

**public void restore( macOnResponse,  blockNumber)**

Restores transfer buffer i.e. copies contents of specified value block to transfer buffer.

**Parameters:**

macOnResponse - false: Response received from card will not be MACed
 true: Response received from card will be MACed

blockNumber - Card value block to be decremented(range 0x00 to 0xFF depending card size)

**Returns:**

void

**Throws:**

com.symbol.emdk.securenfc.MifarePlusSL3Exception

Note:
 1. If sector of specified value block is not already authenticated then restore will fail.
 2. If specified block is not value block then restore will fail.

### transfer

**public void transfer( macOnResponse,  blockNumber)**

Transfers contents of value block stored in transfer buffer to specified
 block.

**Parameters:**

macOnResponse - false: Response received from card will not be MACed
 true: Response received from card will be MACed

blockNumber - Card block whose contents is replaced by transfer buffer(range 0x00 to 0xFF depending card size).

**Returns:**

void

**Throws:**

com.symbol.emdk.securenfc.MifarePlusSL3Exception

Note:
 1. If sector of specified value block is not already authenticated then transfer will fail.
 2. If specified block is not value block then transfer will fail.

### incrementTransfer

**public void incrementTransfer( macOnRsp,  srcblockNumber,  destBlockNumber,  value)**

Performs combined operation of increment() and transfer() on specified value block.
 It stores value of source value block in transfer buffer after adding given value and then copies contents of transfer buffer to destination block.

**Parameters:**

macOnRsp

srcblockNumber - Source block for increment

destBlockNumber - Destination block for transfer

value - Value to be added

**Returns:**

void

**Throws:**

com.symbol.emdk.securenfc.MifarePlusSL3Exception

Note:
 1. If sector of specified value block is not already authenticated then API will fail.
 2. If source block is not value block then API will fail.

### decrementTransfer

**public void decrementTransfer( macOnRsp,  srcblockNo,  dstblockNo,  value)**

Performs combined operation of decrement() and transfer() on specified value block.
 It stores value of source value block in transfer buffer after subtracting given value from it and then copies contents
 of transfer buffer to destination block.

**Parameters:**

macOnRsp

srcblockNo

dstblockNo

value - Value to be subtracted

**Returns:**

void

**Throws:**

com.symbol.emdk.securenfc.MifarePlusSL3Exception

Note:
 1. If sector of specified value block is not already authenticated then API will fail.
 2. If source block is not value block then API will fail.
