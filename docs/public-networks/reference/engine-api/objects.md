---
description: Engine API objects reference
---

# Engine API objects

The following objects are parameters for or returned by the [Engine API methods](index.md).

## Execution payload object

Parameter for [`engine_newPayloadV1`](index.md#engine_newpayloadv1).
Returned by [`engine_getPayloadV1`](index.md#engine_getpayloadv1).

| Key | Type | Value |
|-----|:----:|-------|
| `parentHash`    | *Data*, 32 Bytes      | Hash of the parent block.                                        |
| `feeRecipient`  | *Data*, 20 Bytes      | Beneficiary of the fee.                                          |
| `stateRoot`     | *Data*, 32 Bytes      | Root of the final state trie for the block.                      |
| `receiptsRoot`  | *Data*, 32 Bytes      | Root of the receipts trie for the block.                         |
| `logsBloom`     | *Data*, 256 Bytes     | Bloom filter for light clients to quickly retrieve related logs. |
| `prevRandao`    | *Data*, 32 Bytes      | Difficulty for this block.                                       |
| `blockNumber`   | *Quantity*, 64 Bits   | Block number of block containing this transaction.               |
| `gasLimit`      | *Quantity*, 64 Bits   | Maximum gas allowed in this block.                               |
| `gasUsed`       | *Quantity*, 64 Bits   | Total gas used by all transactions in this block.                |
| `timestamp`     | *Quantity*, 64 Bits   | Unix timestamp (milliseconds) for block assembly.                |
| `extraData`     | *Data*, 0 to 32 Bytes | Extra data field for this block.                                 |
| `baseFeePerGas` | *Quantity*, 256 Bits  | The block's [base fee per gas](../../concepts/transactions/types.md#eip1559-transactions). This field is empty for blocks created before [EIP-1559](https://github.com/ethereum/EIPs/blob/2d8a95e14e56de27c5465d93747b0006bd8ac47f/EIPS/eip-1559.md). |
| `blockHash`     | *Data*, 32 Bytes      | Hash of the execution block.                                     |
| `transactions`  | *Array*               | Array of transaction objects, each object is a list representing `TransactionType`, `TransactionPayload`, or `LegacyTransaction` as defined in [EIP-2718](https://eips.ethereum.org/EIPS/eip-2718). |

## Fork choice state object

Parameter for [`engine_forkchoiceUpdatedV1`](index.md#engine_forkchoiceupdatedv1).

| Key | Type | Value |
|-----|:----:|-------|
| `headBlockHash`      | *Data*, 32 Bytes | Block hash of the head of the canonical chain. |
| `safeBlockHash`      | *Data*, 32 Bytes | "Safe" block hash of the canonical chain under certain synchrony and honesty assumptions. This value MUST be either equal to or an ancestor of `headBlockHash`. |
| `finalizedBlockHash` | *Data*, 32 Bytes | Block hash of the most recent finalized block. |

## Payload attributes object

Parameter for [`engine_forkchoiceUpdatedV1`](index.md#engine_forkchoiceupdatedv1).

| Key | Type | Value |
|-----|:----:|-------|
| `timestamp`             | *Quantity*, 64 Bits | Value for the `timestamp` field of the new payload.              |
| `prevRandao`            | *Data*, 32 Bytes    | Value for the `prevRandao` field of the new payload.             |
| `suggestedFeeRecipient` | *Data*, 20 Bytes     | Suggested value for the `feeRecipient` field of the new payload.|

## Payload status object

Returned by [`engine_newPayloadV1`](index.md#engine_newpayloadv1) and [`engine_forkchoiceUpdatedV1`](index.md#engine_forkchoiceupdatedv1).

| Key | Type | Value |
|-----|:----:|-------|
| `status`          | *Enumeration*    | Either `"VALID"`, `"INVALID"`, `"SYNCING"`, `"ACCEPTED"`, `"INVALID_BLOCK_HASH"`, or `"INVALID_TERMINAL_BLOCK"`. |
| `latestValidHash` | *Data*, 32 Bytes | Hash of the most recent valid block in the branch defined by payload and its ancestors. |
| `validationError` | *String*         | Message providing additional details on the validation error if the payload is classified as `INVALID`, `INVALID_BLOCK_HASH` or `INVALID_TERMINAL_BLOCK`. |

## Transition configuration object

Parameter for and returned by [`engine_exchangeTransitionConfigurationV1`](index.md#engine_exchangetransitionconfigurationv1).

| Key | Type | Value |
|-----|:----:|-------|
| `terminalTotalDifficulty` | *Quantity*, 256 Bits | Maps on the `TERMINAL_TOTAL_DIFFICULTY` parameter of [EIP-3675](https://eips.ethereum.org/EIPS/eip-3675#client-software-configuration). |
| `terminalBlockHash`       | *Data*, 32 Bytes     | Maps on the `TERMINAL_BLOCK_HASH` parameter of [EIP-3675](https://eips.ethereum.org/EIPS/eip-3675#client-software-configuration). |
| `terminalBlockNumber`     | *Quantity*, 64 Bits  | Maps on the `TERMINAL_BLOCK_NUMBER` parameter of [EIP-3675](https://eips.ethereum.org/EIPS/eip-3675#client-software-configuration). |
