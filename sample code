// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SemiPrivateKeyBlockchain {
    // Event to emit transaction details
    event TransactionLogged(
        address indexed sender,
        address indexed receiver,
        bytes32 semiPrivateKey,
        uint256 amount
    );

    // Mapping to simulate balances
    mapping(address => uint256) public balances;

    // Function to hash public keys into semi-private keys
    function generateSemiPrivateKey(bytes32 publicKey) public pure returns (bytes32) {
        // Hashing the public key to create a semi-private key
        return keccak256(abi.encodePacked(publicKey));
    }

    // Function to fund an account (for testing)
    function fundAccount() external payable {
        balances[msg.sender] += msg.value;
    }

    // Function to send funds using semi-private keys
    function sendTransaction(
        bytes32 publicKey, // Public key of the sender
        address receiver,
        uint256 amount
    ) external {
        require(balances[msg.sender] >= amount, "Insufficient balance");
        
        // Generate the semi-private key
        bytes32 semiPrivateKey = generateSemiPrivateKey(publicKey);

        // Deduct the amount from sender's balance
        balances[msg.sender] -= amount;

        // Add the amount to the receiver's balance
        balances[receiver] += amount;

        // Log the transaction with the semi-private key
        emit TransactionLogged(msg.sender, receiver, semiPrivateKey, amount);
    }

    // Function to verify ownership (optional, for testing)
    function verifyOwnership(bytes32 semiPrivateKey, bytes32 publicKey) public pure returns (bool) {
        // Check if the semi-private key matches the hashed public key
        return semiPrivateKey == keccak256(abi.encodePacked(publicKey));
    }
}
