# Overview of SC Procedures

This document aims to give an overview of Qubic SC procedures. The goal is to create wallet connect RPC endpoints to create, sign, and broadcast these transaction types.

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

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