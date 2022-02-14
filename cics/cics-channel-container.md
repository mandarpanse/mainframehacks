# What is IBM CICS Channels and Containers?

The channels and Containers is option provided in CICS to pass huge amount of data between two programs without permanently storing it anywhere.

Channel is nothing but allocated section of "main memory" in CICS to hold data that needs to be passed between two or many programs.

CHANNEL option can be used on API commands like,

LINK
START
XCTL
RETURN TRASNID
GET CONTAINER
PUT CONTAINER
MOVE CONTAINER
DELETE CONTAINER
STARTBROWSE CONTAINER


## How can it be created/read/deleted?

Channel and containers can be created using following API's provided by IBM.

### Creation :
- No need to explicitly create channel.  
- Channel will be created automatically, if it does not exist, on first __PUT CONTAINER__  command. This command requires container name and channel name to be passed for successful execution.

### Read:
- Before reading container, program need to execute __ASSIGN CHANNEL__ command to find the __CHANNEL__ name passed to the program.
- __GET CONTAINER__ command can be used to read the container. This command requires container name and channel name passed for successful execution.

### Deletion:
- __DELETE CONTAINER__ command can be used to delete any container from the channel. This command requires Channel name to be provided along with container name to be deleted.


## Advantages of using Channels and Containers
* No size limit for data transfer.
* No need to explicitly delete channel to free main memory. It happens automatic.
* No need to worry about storage leak as channel will be automatically deleted at the end of the owning task.
* It helps to maintain health of system by eliminating potential of storage leak.
## Disadvantages of using Channels and Containers
* If CHANNEL command is used, SYSID option cannot be used on any of the API Commands to ship it to remote region for execution. 

## Rules:
- Channel/Container name can be maximum 16 characters long.
- Only trailing spaces are allowed in name.
- User defined channels/container names should not start with DFH. It is reserved for CICS created channels and containers.

## Recommendations :
To avoid data mix-up, try to use EIBTASKN as first 5 bytes of Channel name. This will separate that channel from other channels created by same transactions.
