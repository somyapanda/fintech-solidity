# fintech-solidity-homework

This repository contains smart contracts and transactions as part of the Fintech homework assignment Unit 20 - "Looks like we've made our First Contract!". 

As we have created our own Ethereum-compatible blockchain to help connect financial institutions. In this homework assignment, we build smart contracts to automate some company finances to make everyone's lives easier, increase transparency, and to make accounting and auditing practically automatic. We create three `ProfitSplitter` contracts and these contracts will do following things:
    - Pay oue Associate-level employees quickly and easily.
    - Distribute profits to different tiers of employees.
    - Distribute company shares for employees in a "deferred equity incentive plan" automatically.


## Files

* [AssociateProfitSplitter.sol](./AssociateProfitSplitter.sol)
    - file contains an `AssociateProfitSplitter` contract 
    - accept Ether into the contract and divide the Ether evenly among the associate level employees 
    - allow the Human Resources department to pay employees quickly and efficiently
For this section, these are the following tasks:
    - navigate to the [Remix IDE](https://remix.ethereum.org)
    - create a new contract called `AssociateProfitSplitter.sol`
    - At the top of our contract, define the following `public` variables:
        * `employee_one` -- The `address` of the first employee `0x8132DB002e21a53Ef2E1141b21d6A9EC3cEC2749`
        * `employee_two` -- Another `address payable` that represents the second employee `0x2Ff44aB9cb2c8A849ECCC9C2d005817d8356d765`
        * `employee_three` -- The third `address payable` that represents the third employee `0x92B04c9b8AE5f7AdF3D17d1E704c966CC6B5Da89`
    - create a constructor function that accepts:
        * `address payable _one`
        * `address payable _two`
        * `address payable _three`
    - create the following functions:
        * `deposit` -- This function should set to `public payable` check, ensuring that only the owner can call the function.
              * In this function, perform the following steps:
               * Set a `uint amount` to equal `msg.value / 3;` in order to calculate the split value of the Ether.
               * Transfer the `amount` to `employee_one`.
               * Repeat the steps for `employee_two` and `employee_three`.
               * Since `uint` only contains positive whole numbers, and Solidity does not fully support float/decimals, we must deal with a potential remainder at the end of this function since `amount` will discard the remainder during division.
               * We may either have `1` or `2` wei leftover, so transfer the `msg.value - amount * 3` back to `msg.sender`. This will re-multiply the `amount` by 3, then subtract it from the `msg.value` to account for any leftover wei, and send it back to Human Resources.
       * Create a fallback function using `function() external payable`, and call the `deposit` function from within it. This will ensure that the logic in `deposit` executes if Ether is sent directly to the contract. This is important to prevent Ether from being locked in the contract since we don't have a `withdraw` function in this use-case.

![Associate Profit Splitter Smart Contract](./Images/AssociateProfitSplitter/AssociateProfitSplitter_smart_contract.png)

  - amount in addresses that represent `employee_one`, `employee_two`, and `employee_three` before deployment of transaction
![Employee Addresses](./Images/AssociateProfitSplitter/employee_addresses.png)

  - compile the smart contract `AssociateProfitSplitter.sol`
![Smart Contract Compiled](./Images/AssociateProfitSplitter/compiled_contract.png)
![Contract Confirm](./Images/AssociateProfitSplitter/confirm_contract.png)

  - test the contract
       * In Remix, go to `Deploy` tab, deploy the contract to our local `Ganache` chain by connecting to `Injected Web3` and connect MetaMask to `localhost:8545`
![Change Network](./Images/AssociateProfitSplitter/change_network.png)

       * The smart contract is deployed
![Deploy Contract](./Images/AssociateProfitSplitter/deploy_contract.png)

       * The smart contract executes the deposits
![Employee Addresses](./Images/AssociateProfitSplitter/deposit_emp_addresses.png)

![Confirm Deposit](./Images/AssociateProfitSplitter/confirm_deposit.png)

       * The transaction amounts are reflected in the ledger
![Transaction Confirm](./Images/AssociateProfitSplitter/transaction_confirm1.png)

![Transaction Confirmed](./Images/AssociateProfitSplitter/transaction_confirmed.png)


* [TieredProfitSplitter.sol](./TieredProfitSplitter.sol)
    - 