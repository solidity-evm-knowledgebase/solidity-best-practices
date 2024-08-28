# solidity-best-practices

## Contract Layout

- version
- imports
- errors
- interfaces, libraries, contracts
- Type declarations
- State variables
- Events
- Modifiers
- Functions

## Layout of Functions

- constructor
- receive function (if exists)
- fallback function (if exists)
- external
- public
- internal
- private
- view & pure functions (Getter Functions)

## Function Layout

CEI: Checks, Effects, Interactions Pattern

Example: 

```
    function pickWinner() external {
        // Checks
        if (block.timestamp - s_lastTimestamp < i_interval) {
            revert Raffle__RaffleNotOver();
        }
        
        // Effects (Internal Contract State)
        s_raffleState = RaffleState.CALCULATING;

        // Interactions (External Contract interactions)
        uint256 requestId = s_vrfCoordinator.requestRandomWords(
            VRFV2PlusClient.RandomWordsRequest({
                keyHash: i_keyHash,
                subId: i_subscriptionId,
                requestConfirmations: REQUEST_CONFIRMATIONS,
                callbackGasLimit: i_callbackGasLimit,
                numWords: NUM_WORDS,
                extraArgs: VRFV2PlusClient._argsToBytes(
                    // Set nativePayment to true to pay for VRF requests with Sepolia ETH instead of LINK
                    VRFV2PlusClient.ExtraArgsV1({nativePayment: false})
                )
            })
        );
    }

