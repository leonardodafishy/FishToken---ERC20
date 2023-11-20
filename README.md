# FishToken - ERC20 Token Contract

FishToken is an ERC20 token contract facilitating the creation, transfer, and management of tokens. Leveraging the [OpenZeppelin](https://www.openzeppelin.com/) library, it adheres to the ERC20 standard, offering various features and capabilities.

## Features

- **Token Creation**: Generate tokens with a specified name and symbol.
- **Token Transfers**: Facilitate seamless transfers between addresses.
- **Token Burning**: Allow users to burn tokens, reducing the total supply.
- **Token Minting**: Empower the contract owner to mint new tokens.
- **Approval and Delegation**: Enable approval and delegation of token transfers.

## Usage

### Deployment

To deploy the contract, adhere to these steps:

1. Set the Solidity compiler version to at least `0.8`.
2. Import the required `IERC20` interface from the OpenZeppelin library.
3. Deploy the contract by providing the desired `name` and `symbol` for the token.

### Contract Owner

The contract owner possesses special privileges, being the sole entity allowed to execute specific operations. The `onlyOwner` modifier ensures exclusivity:

```solidity
modifier onlyOwner {
    require(msg.sender == _owner, "Only owner is allowed to perform this operation");
    _;
}
```

## Token Information

The contract manages essential information:

- `_name`: The name of the token.
- `_symbol`: The symbol or ticker of the token.
- `_owner`: The address of the contract owner.
- `_totalSupply`: The total supply of tokens.

### Balances

Token balances for each address are tracked using a private mapping:

```solidity
mapping(address => uint256) private _balances;
```

Retrieve an address's balance via the `balanceOf` function:

```solidity
function balanceOf(address account) external view returns (uint256);
```

### Transfers

Tokens transfer between addresses using the `transfer` function. The contract verifies the sender's balance before executing the transfer:

```solidity
function transfer(address to, uint256 value) public returns (bool);
```

### Burning Tokens

Burning tokens is achievable through the `burn` function, diminishing the total supply:

```solidity
function burn(uint256 value) public returns (bool);
```

### Minting Tokens

The contract owner mints new tokens via the `mint` function:

```solidity
function mint(address to, uint256 value) public onlyOwner returns (bool);
```

### Approvals and Allowances

Delegating token transfers involves the `approve` function, granting an address permission to spend a designated token amount:

```solidity
function approve(address spender, uint256 value) external returns (bool);
```

Access allowances through the `allowances` function:

```solidity
function allowance(address owner, address spender) external view returns (uint256);
```

Transfer tokens on behalf of another address using the `transferFrom` function:

```solidity
function transferFrom(address from, address to, uint256 value) external returns (bool);
```

## Events

The contract emits key events:

- `Transfer`: Triggered during token transfers.
- `Approval`: Triggered upon approval for token transfers.
- `Burn`: Triggered when users erase tokens.
- `Mint`: Triggered during token minting.

## Errors

Custom errors handle exceptional scenarios:

- `InvalidReceiver`: Raised for an invalid receiver address (0x0).
- `InsufficientBalance`: Raised when a sender lacks the balance for a transfer or burn.
- `InsufficientAllowance`: Raised when the allowance is insufficient for a `transferFrom` operation.

These errors provide meaningful feedback during exceptional conditions.

## License

This contract operates under the [MIT License](https://opensource.org/licenses/MIT). Refer to the SPDX-License-Identifier comment at the contract's outset for detailed license information.

## Author
This project is authored by Miguel Angelo M. Fesalbon.
