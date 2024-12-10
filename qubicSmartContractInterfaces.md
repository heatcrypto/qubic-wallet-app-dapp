# Overview of SC Procedures

This document aims to give an overview of Qubic SC procedures. The goal is to create wallet connect RPC endpoints to create, sign, and broadcast these transaction types.

## Qx

Implementation: [Qx.h](https://github.com/qubic/core/blob/main/src/contracts/Qx.h)

### IssueAsset

`REGISTER_USER_PROCEDURE(IssueAsset, 1);`

```cpp
struct IssueAsset_input
{
    uint64 assetName;
    sint64 numberOfShares;
    uint64 unitOfMeasurement;
    sint8 numberOfDecimalPlaces;
};
struct IssueAsset_output
{
    sint64 issuedNumberOfShares;
};
```

#### Proposed Interface

Rpc identifier `qubic_qx_IssueAsset`

| Property               | Type    | Value                            |
|------------------------|---------|----------------------------------|
| assetName              | String  | Unique asset name                |
| numberOfShares         | String  | Total number of shares to issue  |
| unitOfMeasurement      | Number  | Unit of measurement              |
| numberOfDecimalPlaces  | Number  | Number of decimal places to use  |

On success, the following object is returned.

```ts
interface IssueAssetResult {
    issuedNumberOfShares: number;
}
```

### TransferShareOwnershipAndPossession

`REGISTER_USER_PROCEDURE(TransferShareOwnershipAndPossession, 2);`

```cpp
struct TransferShareOwnershipAndPossession_input
{
    id issuer;
    id newOwnerAndPossessor;
    uint64 assetName;
    sint64 numberOfShares;
};
struct TransferShareOwnershipAndPossession_output
{
    sint64 transferredNumberOfShares;
};
```

#### Proposed Interface

Rpc identifier `qubic_qx_TransferShareOwnershipAndPossession`

| Property              | Type    | Value                                     |
|-----------------------|---------|-------------------------------------------|
| issuer                | String  | The current owner's public key            |
| newOwnerAndPossessor  | String  | The new owner's public key                |
| assetName             | String  | Unique asset name identifier              |
| numberOfShares        | String  | Number of shares to transfer              |

On success, the following object is returned.

```ts
interface TransferShareOwnershipAndPossessionResult {
    transferredNumberOfShares: number;
}
```


### AddToAskOrder

`REGISTER_USER_PROCEDURE(AddToAskOrder, 5);`

```cpp
struct AddToAskOrder_input
{
    id issuer;
    uint64 assetName;
    sint64 price;
    sint64 numberOfShares;
};
struct AddToAskOrder_output
{
    sint64 addedNumberOfShares;
};
```

#### Proposed Interface

Rpc identifier `qubic_qx_AddToAskOrder`

| Property         | Type    | Value                                 |
|------------------|---------|---------------------------------------|
| issuer           | String  | Public key of the order issuer        |
| assetName        | String  | Unique asset name identifier          |
| price            | String  | Price per share in the ask order      |
| numberOfShares   | String  | Number of shares to add to the order  |

On success, the following object is returned.

```ts
interface AddToAskOrderResult {
    addedNumberOfShares: number;
}
```


### AddToBidOrder

`REGISTER_USER_PROCEDURE(AddToBidOrder, 6);`

```cpp
struct AddToBidOrder_input
{
    id issuer;
    uint64 assetName;
    sint64 price;
    sint64 numberOfShares;
};
struct AddToBidOrder_output
{
    sint64 addedNumberOfShares;
};
```

#### Proposed Interface

Rpc identifier `qubic_qx_AddToBidOrder`

| Property         | Type    | Value                                |
|------------------|---------|--------------------------------------|
| issuer           | String  | Public key of the order issuer       |
| assetName        | String  | Unique asset name identifier         |
| price            | String  | Price per share in the bid order     |
| numberOfShares   | String  | Number of shares to add to the bid   |

On success, the following object is returned.

```ts
interface AddToBidOrderResult {
    addedNumberOfShares: number;
}
```


### RemoveFromAskOrder

`REGISTER_USER_PROCEDURE(RemoveFromAskOrder, 7);`

```cpp
struct RemoveFromAskOrder_input
{
    id issuer;
    uint64 assetName;
    sint64 price;
    sint64 numberOfShares;
};
struct RemoveFromAskOrder_output
{
    sint64 removedNumberOfShares;
};
```

#### Proposed Interface

Rpc identifier `qubic_qx_RemoveFromAskOrder`

| Property         | Type    | Value                                     |
|------------------|---------|-------------------------------------------|
| issuer           | String  | Public key of the order issuer            |
| assetName        | String  | Unique asset name identifier              |
| price            | String  | Price per share in the ask order          |
| numberOfShares   | String  | Number of shares to remove from the order |

On success, the following object is returned.

```ts
interface RemoveFromAskOrderResult {
    removedNumberOfShares: number;
}
```


### RemoveFromBidOrder

`REGISTER_USER_PROCEDURE(RemoveFromBidOrder, 8);`

```cpp
struct RemoveFromBidOrder_input
{
    id issuer;
    uint64 assetName;
    sint64 price;
    sint64 numberOfShares;
};
struct RemoveFromBidOrder_output
{
    sint64 removedNumberOfShares;
};
```

#### Proposed Interface

Rpc identifier `qubic_qx_RemoveFromBidOrder`

| Property         | Type    | Value                                     |
|------------------|---------|-------------------------------------------|
| issuer           | String  | Public key of the order issuer            |
| assetName        | String  | Unique asset name identifier              |
| price            | String  | Price per share in the bid order          |
| numberOfShares   | String  | Number of shares to remove from the order |

On success, the following object is returned.

```ts
interface RemoveFromBidOrderResult {
    removedNumberOfShares: number;
}
```


## Qearn

Source: [Qearn.h](https://github.com/qubic/core/blob/main/src/contracts/Qearn.h)

### lock

`REGISTER_USER_PROCEDURE(lock, 1);`

```cpp
struct lock_input
{
};
struct lock_output
{
    sint32 returnCode;
};
```

#### Proposed Interface

Rpc identifier `qubic_qearn_lock`

| Property  | Type    | Value            |
|-----------|---------|------------------|
| (none)    | (none)  | No input fields  |

On success, the following object is returned.

```ts
interface LockResult {
    returnCode: number;
}
```


### unlock

`REGISTER_USER_PROCEDURE(unlock, 2);`

```cpp
struct unlock_input
{
    uint64 amount;
    uint32 lockedEpoch;
};
struct unlock_output
{
    sint32 returnCode;
};
```

#### Proposed Interface

Rpc identifier `qubic_qearn_unlock`

| Property      | Type    | Value                       |
|---------------|---------|-----------------------------|
| amount        | String  | Amount to unlock            |
| lockedEpoch   | Number  | Epoch during which it was locked |

On success, the following object is returned.

```ts
interface UnlockResult {
    returnCode: number;
}
```

## Quottery

Implementation: [Quottery.h](https://github.com/qubic/core/blob/main/src/contracts/Quottery.h)

### issueBet

`REGISTER_USER_PROCEDURE(issueBet, 1);`

```cpp
struct issueBet_input
{
    id betDesc;
    id_8 optionDesc;
    id_8 oracleProviderId;
    uint32_8 oracleFees;
    uint32 closeDate;
    uint32 endDate;
    uint64 amountPerSlot;
    uint32 maxBetSlotPerOption;
    uint32 numberOfOption;
};
struct issueBet_output
{
};
```

#### Proposed Interface

Rpc identifier `qubic_quottery_issueBet`

| Property            | Type    | Value                                       |
|---------------------|---------|---------------------------------------------|
| betDesc             | String  | Description of the bet                     |
| optionDesc          | String  | Options available for betting              |
| oracleProviderId    | String  | ID of the oracle provider                  |
| oracleFees          | String  | Fees associated with the oracle provider   |
| closeDate           | Number  | Timestamp for when betting closes          |
| endDate             | Number  | Timestamp for when the bet ends            |
| amountPerSlot       | String  | Amount required per betting slot           |
| maxBetSlotPerOption | Number  | Maximum slots available per option         |
| numberOfOption      | Number  | Number of options available for the bet    |

On success, the following object is returned.

```ts
interface IssueBetResult {
    // No fields in the output struct
}
```


### joinBet

`REGISTER_USER_PROCEDURE(joinBet, 2);`

```cpp
struct joinBet_input
{
    uint32 betId;
    uint32 numberOfSlot;
    uint32 option;
    uint32 _placeHolder;
};
struct joinBet_output
{
};
```

#### Proposed Interface

Rpc identifier `qubic_quottery_joinBet`

| Property         | Type    | Value                             |
|------------------|---------|-----------------------------------|
| betId            | Number  | Identifier of the bet            |
| numberOfSlot     | Number  | Number of slots to join          |
| option           | Number  | Option selected for the bet      |
| _placeHolder     | Number  | Placeholder (reserved)           |

On success, the following object is returned.

```ts
interface JoinBetResult {
    // No fields in the output struct
}
```


### cancelBet

`REGISTER_USER_PROCEDURE(cancelBet, 3);`

```cpp
struct cancelBet_input
{
    uint32 betId;
};
struct cancelBet_output
{
};
```

#### Proposed Interface

Rpc identifier `qubic_quottery_cancelBet`

| Property   | Type    | Value                  |
|------------|---------|------------------------|
| betId      | Number  | Identifier of the bet  |

On success, the following object is returned.

```ts
interface CancelBetResult {
    // No fields in the output struct
}
```


### publishResult

`REGISTER_USER_PROCEDURE(publishResult, 4);`

```cpp
struct publishResult_input
{
    uint32 betId;
    uint32 option;
};
struct publishResult_output
{
};
```

#### Proposed Interface

Rpc identifier `qubic_quottery_publishResult`

| Property   | Type    | Value                               |
|------------|---------|-------------------------------------|
| betId      | Number  | Identifier of the bet               |
| option     | Number  | Option selected as the result       |

On success, the following object is returned.

```ts
interface PublishResultResult {
    // No fields in the output struct
}
```

## QVault

Implementation: [QVAULT.h](https://github.com/qubic/core/blob/main/src/contracts/QVAULT.h)

### submitAuthAddress

`REGISTER_USER_PROCEDURE(submitAuthAddress, 1);`

```cpp
struct submitAuthAddress_input 
{
    id newAddress;
};

struct submitAuthAddress_output
{
};
```

#### Proposed Interface

Rpc identifier `qubic_qvault_submitAuthAddress`

| Property     | Type    | Value                                    |
|--------------|---------|------------------------------------------|
| newAddress   | String  | Address to be submitted for authorization |

On success, the following object is returned.

```ts
interface SubmitAuthAddressResult {
    // No fields in the output struct
}
```


### changeAuthAddress

`REGISTER_USER_PROCEDURE(changeAuthAddress, 2);`

```cpp
struct changeAuthAddress_input
{
    uint32 numberOfChangedAddress;
};

struct changeAuthAddress_output
{
};
```

#### Proposed Interface

Rpc identifier `qubic_qvault_changeAuthAddress`

| Property                | Type    | Value                                  |
|-------------------------|---------|----------------------------------------|
| numberOfChangedAddress  | Number  | Number of addresses to be changed      |

On success, the following object is returned.

```ts
interface ChangeAuthAddressResult {
    // No fields in the output struct
}
```


### submitDistributionPermille

`REGISTER_USER_PROCEDURE(submitDistributionPermille, 3);`

```cpp
struct submitDistributionPermille_input
{
    uint32 newQCAPHolderPermille;
    uint32 newReinvestingPermille;
    uint32 newDevPermille;
};

struct submitDistributionPermille_output
{
};
```

#### Proposed Interface

Rpc identifier `qubic_qvault_submitDistributionPermille`

| Property                 | Type    | Value                                        |
|--------------------------|---------|----------------------------------------------|
| newQCAPHolderPermille    | Number  | Permille value for QCAP holder distribution  |
| newReinvestingPermille   | Number  | Permille value for reinvesting distribution  |
| newDevPermille           | Number  | Permille value for developer distribution    |

On success, the following object is returned.

```ts
interface SubmitDistributionPermilleResult {
    // No fields in the output struct
}
```


### changeDistributionPermille

`REGISTER_USER_PROCEDURE(changeDistributionPermille, 4);`

```cpp
struct changeDistributionPermille_input
{
    uint32 newQCAPHolderPermille;
    uint32 newReinvestingPermille;
    uint32 newDevPermille;
};

struct changeDistributionPermille_output
{
};
```

#### Proposed Interface

Rpc identifier `qubic_qvault_changeDistributionPermille`

| Property                 | Type    | Value                                        |
|--------------------------|---------|----------------------------------------------|
| newQCAPHolderPermille    | Number  | Permille value for QCAP holder distribution  |
| newReinvestingPermille   | Number  | Permille value for reinvesting distribution  |
| newDevPermille           | Number  | Permille value for developer distribution    |

On success, the following object is returned.

```ts
interface ChangeDistributionPermilleResult {
    // No fields in the output struct
}
```


### submitReinvestingAddress

`REGISTER_USER_PROCEDURE(submitReinvestingAddress, 5);`

```cpp
struct submitReinvestingAddress_input
{
    id newAddress;
};

struct submitReinvestingAddress_output
{
};
```

#### Proposed Interface

Rpc identifier `qubic_qvault_submitReinvestingAddress`

| Property     | Type    | Value                                    |
|--------------|---------|------------------------------------------|
| newAddress   | String  | Address to be submitted for reinvesting  |

On success, the following object is returned.

```ts
interface SubmitReinvestingAddressResult {
    // No fields in the output struct
}
```


### changeReinvestingAddress

`REGISTER_USER_PROCEDURE(changeReinvestingAddress, 6);`

```cpp
struct changeReinvestingAddress_input
{
    id newAddress;
};

struct changeReinvestingAddress_output
{
};
```

#### Proposed Interface

Rpc identifier `qubic_qvault_changeReinvestingAddress`

| Property     | Type    | Value                                 |
|--------------|---------|---------------------------------------|
| newAddress   | String  | Address to be changed for reinvesting |

On success, the following object is returned.

```ts
interface ChangeReinvestingAddressResult {
    // No fields in the output struct
}
```


### submitAdminAddress

`REGISTER_USER_PROCEDURE(submitAdminAddress, 7);`

```cpp
struct submitAdminAddress_input
{
    id newAddress;
};

struct submitAdminAddress_output
{
};
```

#### Proposed Interface

Rpc identifier `qubic_qvault_submitAdminAddress`

| Property     | Type    | Value                              |
|--------------|---------|------------------------------------|
| newAddress   | String  | Address to be submitted as admin   |

On success, the following object is returned.

```ts
interface SubmitAdminAddressResult {
    // No fields in the output struct
}
```


### changeAdminAddress

`REGISTER_USER_PROCEDURE(changeAdminAddress, 8);`

```cpp
struct changeAdminAddress_input
{
    id newAddress;
};

struct changeAdminAddress_output
{
};
```

#### Proposed Interface

Rpc identifier `qubic_qvault_changeAdminAddress`

| Property     | Type    | Value                              |
|--------------|---------|------------------------------------|
| newAddress   | String  | Address to be changed as admin     |

On success, the following object is returned.

```ts
interface ChangeAdminAddressResult {
    // No fields in the output struct
}
```


### submitBannedAddress

`REGISTER_USER_PROCEDURE(submitBannedAddress, 9);`

```cpp
struct submitBannedAddress_input
{
    id bannedAddress;
};

struct submitBannedAddress_output
{
};
```

#### Proposed Interface

Rpc identifier `qubic_qvault_submitBannedAddress`

| Property        | Type    | Value                                |
|-----------------|---------|--------------------------------------|
| bannedAddress   | String  | Address to be submitted as banned   |

On success, the following object is returned.

```ts
interface SubmitBannedAddressResult {
    // No fields in the output struct
}
```


### saveBannedAddress

`REGISTER_USER_PROCEDURE(saveBannedAddress, 10);`

```cpp
struct saveBannedAddress_input
{
    id bannedAddress;
};

struct saveBannedAddress_output
{
};
```

#### Proposed Interface

Rpc identifier `qubic_qvault_saveBannedAddress`

| Property        | Type    | Value                             |
|-----------------|---------|-----------------------------------|
| bannedAddress   | String  | Address to be saved as banned    |

On success, the following object is returned.

```ts
interface SaveBannedAddressResult {
    // No fields in the output struct
}
```


### submitUnbannedAddress

`REGISTER_USER_PROCEDURE(submitUnbannedAddress, 11);`

```cpp
struct submitUnbannedAddress_input
{
    id unbannedAddress;
};

struct submitUnbannedAddress_output
{
};
```

#### Proposed Interface

Rpc identifier `qubic_qvault_submitUnbannedAddress`

| Property          | Type    | Value                                   |
|-------------------|---------|-----------------------------------------|
| unbannedAddress   | String  | Address to be submitted as unbanned     |

On success, the following object is returned.

```ts
interface SubmitUnbannedAddressResult {
    // No fields in the output struct
}
```


### unblockBannedAddress

`REGISTER_USER_PROCEDURE(unblockBannedAddress, 12);`

```cpp
struct unblockBannedAddress_input
{
    id unbannedAddress;
};

struct unblockBannedAddress_output
{
};
```

#### Proposed Interface

Rpc identifier `qubic_qvault_unblockBannedAddress`

| Property          | Type    | Value                                 |
|-------------------|---------|---------------------------------------|
| unbannedAddress   | String  | Address to be unblocked              |

On success, the following object is returned.

```ts
interface UnblockBannedAddressResult {
    // No fields in the output struct
}
```