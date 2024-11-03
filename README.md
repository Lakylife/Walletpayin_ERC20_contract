# WPAYIN Smart Contract

##OFFICIAL CONTRACT:## 0x28450F5b5576c19cc1FD90fA84EDcf893d136624

## Overview
The **WPAYIN** smart contract represents an ERC-20 token called **WPAYIN** (symbol: **WPI**). WPAYIN serves as a cross-chain wallet solution, bridging blockchain ecosystems like Ethereum, TON, and Bitcoin, and offering users a unified, seamless experience.

The contract implements essential ERC-20 functions, along with custom transaction fees, wallet and transfer limits, and Uniswap liquidity integration.

## Token Details
- **Name**: WPAYIN
- **Symbol**: WPI
- **Decimals**: 9
- **Total Supply**: 100,000,000 WPI

## Key Components

### Libraries
- **SafeMath**: Provides safe arithmetic operations (addition, subtraction, multiplication, division) to prevent overflow errors.

### Interfaces
- **IERC20**: Defines the ERC-20 standard functions for token transfers, approvals, and balance checks.
- **IUniswapV2Factory**: Interface for Uniswap’s factory, used to create token pairs.
- **IUniswapV2Router02**: Interface for Uniswap’s router, enabling token swaps and liquidity functions.

### Contracts

1. **Context**: Provides information about the current execution context, including the sender of the transaction.
2. **Ownable**: Adds an owner role with specific permissions like setting fees and opening trading. This contract includes functions to transfer or renounce ownership.
3. **WPAYIN**: The main contract implementing the ERC-20 standard and additional functionality for WPAYIN tokens:
   - **ERC-20 Functions**: Includes `transfer`, `approve`, and `transferFrom` for standard token interactions.
   - **Custom Modifiers**:
     - `checkMaxWallet`: Enforces a maximum holding per wallet.
     - `checkMaxTransfer`: Limits maximum transfer amount per transaction.
     - `lockTheSwap`: Prevents reentrancy attacks during swap operations.
   - **Events**:
     - `MaxTxAmountUpdated`: Emitted when the max transaction limit is updated.
     - `TransferTaxUpdated`: Emitted when the transaction fee is changed.
     - `FeesCollected`: Emitted whenever transaction fees are collected.
     - `FeeRecipient2Updated`: Emitted when the secondary fee recipient is changed.
     - `LimitsRemoved`: Emitted when max wallet and transfer limits are removed.

## Main Functionalities

### Fees and Limits
- **Transaction Fees**: 3% transaction fee on each transfer, split equally between two predefined addresses (`feeRecipient1` and `feeRecipient2`).
- **Maximum Wallet Limit**: Each wallet can hold no more than 1% of the total token supply.
- **Maximum Transaction Limit**: Limits each transfer to a maximum of 1% of the total supply.

### Uniswap Integration and Trading
- **openTrading**: Enables trading on Uniswap by creating a WPI-ETH pair and adding initial liquidity.
  - Sets `tradingOpen` to `true` and enables `swapEnabled`.
  - Adds 2 ETH and 60% of the total token supply to the Uniswap pool.
- **swapExactTokensForETHSupportingFeeOnTransferTokens**: Supports Uniswap token swaps with fees applied to each transfer.

### Owner Functions
- **setMaxWalletSize**: Updates the maximum wallet size.
- **setMaxTransferSize**: Updates the maximum transfer size.
- **excludeFromFees**: Excludes specific addresses from transaction fees.
- **setTransactionFee**: Modifies the transaction fee, capped at 100% as a safeguard.
- **setFeeRecipient2**: Updates the secondary fee recipient.
- **removeLimits**: Removes max wallet size and transfer size restrictions.

## Additional Security
The contract uses the `SafeMath` library to prevent overflow errors and adheres to the **Checks-Effects-Interactions** pattern, ensuring state changes occur before external calls to minimize reentrancy risks.

## Contract Summary
The WPAYIN contract provides a flexible token system with built-in liquidity and fee management, designed to facilitate secure trading on decentralized exchanges. The WPAYIN ecosystem is adaptable for cross-chain integration, enhancing user experience while maintaining security and stability.

---

For more information, visit the [WPAYIN Documentation](https://docs.walletpayin.com).
