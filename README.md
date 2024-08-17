# Vault Smart Contract

The `Vault` smart contract allows users to deposit and withdraw ERC-20 tokens in exchange for shares, which represent ownership of the assets held in the vault. This contract is designed to provide a mechanism for pooling and distributing tokens among participants.

## Features

- **Deposit Tokens:** Users can deposit ERC-20 tokens into the vault and receive shares proportional to their deposit.
- **Withdraw Tokens:** Users can withdraw their tokens by redeeming their shares.

## Contract Details

- **Token:** The ERC-20 token being used in the vault is specified during contract deployment.
- **Shares:** Shares are minted upon deposit and represent the user's claim on the vault's assets. These shares can later be redeemed for the corresponding amount of tokens.

## Functions

### `constructor(address _token)`

This constructor initializes the `Vault` contract by setting the ERC-20 token that will be managed by the vault.

- `_token`: The address of the ERC-20 token contract.

### `deposit(uint _amount) external`

This function allows users to deposit ERC-20 tokens into the vault.

- `_amount`: The amount of tokens to deposit.

**How it works:**

- If the vault is empty (i.e., `totalSupply` is 0), the deposited amount directly determines the shares minted.
- If the vault already has deposits, the number of shares minted is proportional to the user's deposit relative to the total balance of the vault.

### `withdraw(uint _shares) external`

This function allows users to withdraw their tokens by redeeming their shares.

- `_shares`: The number of shares to redeem.

**How it works:**

- The amount of tokens withdrawn is proportional to the user's share of the total supply.
- The user's shares are burned, reducing their ownership of the vault.

### Internal Functions

#### `_mint(address _to, uint _shares) private`

Mints new shares and assigns them to the specified address.

- `_to`: The address to receive the newly minted shares.
- `_shares`: The number of shares to mint.

#### `_burn(address _from, uint _shares) private`

Burns the specified number of shares from the specified address.

- `_from`: The address from which to burn the shares.
- `_shares`: The number of shares to burn.

## Example Workflow

1. **Deploy the Contract**: Deploy the `Vault` contract, specifying the ERC-20 token that will be managed.
2. **Deposit Tokens**: Call the `deposit()` function to deposit tokens into the vault. The user receives shares representing their deposit.
3. **Withdraw Tokens**: Call the `withdraw()` function to redeem your shares and receive the corresponding amount of tokens.

## Security Considerations

- **Immutable Token Address:** The address of the ERC-20 token is immutable, ensuring that the vault only manages the specified token.
- **Proportional Shares:** The minting and burning of shares ensure that the user's ownership is always proportional to the total assets in the vault.

## License

This project is licensed under the MIT License.


# ERC20 Smart Contract

This project implements a basic ERC-20 token in Solidity. The contract includes the standard functionality of an ERC-20 token, such as transferring tokens, approving allowances, and minting or burning tokens. The token is named "Solidity by Example" with the symbol "SOLBYEX" and follows the ERC-20 token standard.

## Features

- **Token Transfers:** Transfer tokens between addresses.
- **Allowance and Transfer From:** Approve an address to spend a certain amount of tokens on behalf of the token owner and execute transfers.
- **Minting:** Create new tokens and add them to the total supply.
- **Burning:** Destroy tokens, reducing the total supply.

## Contract Details

- **Token Name:** Solidity by Example
- **Symbol:** SOLBYEX
- **Decimals:** 18 (standard for ERC-20 tokens)
- **Total Supply:** The total amount of tokens in circulation.

## Functions

### `transfer(address recipient, uint amount) external returns (bool)`

Transfers tokens from the caller's account to the specified `recipient`.

- `recipient`: The address to receive the tokens.
- `amount`: The number of tokens to transfer.

**Returns:** `true` if the transfer is successful.

### `approve(address spender, uint amount) external returns (bool)`

Approves `spender` to spend up to `amount` of the caller's tokens.

- `spender`: The address that will be allowed to spend the tokens.
- `amount`: The maximum number of tokens the `spender` is allowed to spend.

**Returns:** `true` if the approval is successful.

### `transferFrom(address sender, address recipient, uint amount) external returns (bool)`

Transfers tokens from `sender` to `recipient` using the allowance mechanism. The caller must have approval to spend the tokens.

- `sender`: The address to transfer tokens from.
- `recipient`: The address to transfer tokens to.
- `amount`: The number of tokens to transfer.

**Returns:** `true` if the transfer is successful.

### `mint(uint amount) external`

Mints new tokens and assigns them to the caller's account. This increases the total supply of the token.

- `amount`: The number of tokens to mint.

### `burn(uint amount) external`

Burns tokens from the caller's account, reducing the total supply.

- `amount`: The number of tokens to burn.

## Events

### `Transfer(address indexed from, address indexed to, uint value)`

Emitted when tokens are transferred, including zero value transfers.

- `from`: The address tokens are transferred from.
- `to`: The address tokens are transferred to.
- `value`: The number of tokens transferred.

### `Approval(address indexed owner, address indexed spender, uint value)`

Emitted when the allowance of a `spender` for an `owner` is set by a call to `approve`. `value` is the new allowance.

- `owner`: The address that owns the tokens.
- `spender`: The address approved to spend the tokens.
- `value`: The amount of tokens that can be spent.

## Example Usage

1. **Deploy the Contract**: Deploy the `ERC20` contract to an Ethereum network.
2. **Mint Tokens**: Use the `mint()` function to create new tokens.
3. **Transfer Tokens**: Call `transfer()` to send tokens to another address.
4. **Approve and Transfer From**: Approve an address to spend tokens on your behalf and then execute a transfer using `transferFrom()`.
5. **Burn Tokens**: Use the `burn()` function to reduce the supply of tokens.

## Security Considerations

- **Overflow Protection:** Ensure that proper validations are in place to avoid overflows when transferring, minting, or burning tokens.
- **Allowance Risks:** Be cautious when setting allowances to avoid scenarios like the "ERC20 race condition" issue.

## License

This project is licensed under the MIT License.
