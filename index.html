// SPDX-License-Identifier: MIT
pragma solidity ^0.8.19;

/**
 * @title Monad Yield Migrator
 * @dev Cross-chain yield optimization using MetaMask Smart Accounts & Delegation
 * Features:
 * - MetaMask Smart Account integration
 * - Permission-based delegation system
 * - Cross-chain yield migration (Monad + Base + Arbitrum)
 * - Gas-aware optimization
 * - Envio monitoring integration
 */
contract MonadYieldMigrator {
    
    // Delegation configuration
    struct MigrationConfig {
        address user;                    // MetaMask Smart Account owner
        address agent;                   // Authorized delegate
        uint256 maxAmount;              // Maximum amount agent can move
        string[] allowedChains;         // Chains agent can operate on
        uint256 minAPYGain;             // Minimum APY gain to trigger migration
        uint256 cooldownPeriod;         // Time between migrations
        bool isActive;                  // Whether automation is active
        uint256 lastMigration;          // Timestamp of last migration
        uint256 totalOptimized;         // Total value optimized
    }
    
    // State variables
    mapping(address => MigrationConfig) public migrations;
    uint256 public totalUsers;
    uint256 public totalOptimizations;
    
    // Events for frontend and Envio monitoring
    event SmartAccountLinked(address indexed user);
    event MigrationDelegationCreated(
        address indexed user,
        address indexed agent,
        uint256 maxAmount,
        uint256 minAPYGain,
        uint256 cooldownPeriod
    );
    event YieldOptimized(
        address indexed user,
        string fromChain,
        string toChain,
        uint256 amount,
        uint256 netGain,
        uint256 timestamp
    );
    event AutomationPaused(address indexed user);
    event DelegationRevoked(address indexed user);
    
    /**
     * @dev Link user's MetaMask Smart Account to the system
     */
    function linkSmartAccount() external {
        require(migrations[msg.sender].user == address(0), "Account already linked");
        
        migrations[msg.sender] = MigrationConfig({
            user: msg.sender,
            agent: address(0),
            maxAmount: 0,
            allowedChains: new string[](0),
            minAPYGain: 0,
            cooldownPeriod: 0,
            isActive: false,
            lastMigration: 0,
            totalOptimized: 0
        });
        
        totalUsers++;
        emit SmartAccountLinked(msg.sender);
    }
    
    /**
     * @dev Create delegation for automated yield migration
     * @param agent Address authorized to execute migrations
     * @param maxAmount Maximum amount agent can move
     * @param allowedChains Array of chain names agent can operate on
     * @param minAPYGain Minimum APY gain required (in basis points)
     * @param cooldownPeriod Minimum time between migrations
     */
    function createMigrationDelegation(
        address agent,
        uint256 maxAmount,
        string[] calldata allowedChains,
        uint256 minAPYGain,
        uint256 cooldownPeriod
    ) external {
        MigrationConfig storage config = migrations[msg.sender];
        require(config.user == msg.sender, "Smart account not linked");
        require(agent != address(0), "Invalid agent address");
        require(maxAmount > 0, "Max amount must be positive");
        require(allowedChains.length > 0, "Must allow at least one chain");
        require(minAPYGain >= 50, "Minimum 0.5% APY gain required"); // 50 basis points
        
        config.agent = agent;
        config.maxAmount = maxAmount;
        config.allowedChains = allowedChains;
        config.minAPYGain = minAPYGain;
        config.cooldownPeriod = cooldownPeriod;
        config.isActive = true;
        
        emit MigrationDelegationCreated(
            msg.sender,
            agent,
            maxAmount,
            minAPYGain,
            cooldownPeriod
        );
    }
    
    /**
     * @dev Execute yield optimization (called by authorized agent)
     * @param user Smart Account owner
     * @param fromChain Source chain name
     * @param toChain Target chain name
     * @param amount Amount being migrated
     * @param netGain Net APY gain after gas costs (basis points)
     */
    function executeOptimization(
        address user,
        string calldata fromChain,
        string calldata toChain,
        uint256 amount,
        uint256 netGain
    ) external {
        MigrationConfig storage config = migrations[user];
        
        // Authorization checks
        require(config.isActive, "Migration not active");
        require(msg.sender == config.agent, "Not authorized agent");
        require(amount <= config.maxAmount, "Amount exceeds delegation limit");
        require(netGain >= config.minAPYGain, "Insufficient gain");
        require(block.timestamp >= config.lastMigration + config.cooldownPeriod, "In cooldown");
        
        // Chain permission checks
        bool fromChainAllowed = false;
        bool toChainAllowed = false;
        for(uint i = 0; i < config.allowedChains.length; i++) {
            if(keccak256(abi.encodePacked(config.allowedChains[i])) == keccak256(abi.encodePacked(fromChain))) {
                fromChainAllowed = true;
            }
            if(keccak256(abi.encodePacked(config.allowedChains[i])) == keccak256(abi.encodePacked(toChain))) {
                toChainAllowed = true;
            }
        }
        require(fromChainAllowed, "Source chain not allowed");
        require(toChainAllowed, "Target chain not allowed");
        
        // Update state
        config.lastMigration = block.timestamp;
        config.totalOptimized += amount;
        totalOptimizations++;
        
        // Emit event for Envio monitoring
        emit YieldOptimized(
            user,
            fromChain,
            toChain,
            amount,
            netGain,
            block.timestamp
        );
    }
    
    /**
     * @dev Pause automation (user can restart by creating new delegation)
     */
    function pauseAutomation() external {
        migrations[msg.sender].isActive = false;
        emit AutomationPaused(msg.sender);
    }
    
    /**
     * @dev Revoke delegation completely
     */
    function revokeDelegation() external {
        migrations[msg.sender].agent = address(0);
        migrations[msg.sender].isActive = false;
        emit DelegationRevoked(msg.sender);
    }
    
    /**
     * @dev Get user's migration configuration
     */
    function getUserConfig(address user) external view returns (
        address agent,
        uint256 maxAmount,
        string[] memory allowedChains,
        uint256 minAPYGain,
        uint256 cooldownPeriod,
        bool isActive,
        uint256 lastMigration,
        uint256 totalOptimized
    ) {
        MigrationConfig memory config = migrations[user];
        return (
            config.agent,
            config.maxAmount,
            config.allowedChains,
            config.minAPYGain,
            config.cooldownPeriod,
            config.isActive,
            config.lastMigration,
            config.totalOptimized
        );
    }
    
    /**
     * @dev Get contract statistics for Envio dashboard
     */
    function getStats() external view returns (
        uint256 userCount,
        uint256 optimizationCount,
        uint256 totalValueOptimized
    ) {
        return (totalUsers, totalOptimizations, 0); // totalValueOptimized would require tracking
    }
}
