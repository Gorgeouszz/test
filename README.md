# test
a noob's practice

pragma solidity ^0.6.0;

contract ERC20 {
    
    uint256 private _totalSupply;
    mapping (address => uint256) _balances;
    mapping (address => mapping(address => uint256)) private _allowance;
    string private _name;
    string private _symbol;
    uint8 private _decimals;
    
    constructor(string memory _myname, string memory _mysymbol,uint8 _mydecimals, uint256 _mytotalsupply ) public {
        _name = _myname;
        _symbol = _mysymbol;
        _decimals = _mydecimals;
        _totalSupply = _mytotalsupply;
    }
    
    event Transfer(address indexed from, address indexed to, uint256 value);
    
    function name() public view returns (string memory) {
        return _name;
    }
    
    function symbol() public view returns (string memory) {
        return _symbol;
    }
    
    function decimals() public view returns (uint8) {
        return _decimals;
    }
    
    function totalSupply() public view returns (uint256) {
        return _totalSupply;
    }
    
    function balanceof(address account) public view returns (uint256) {
        return _balances[account];
    }
    
    function allowance(address owner, address spender) public view returns (uint256) {
        return _allowance[owner][spender];
    }
    
    function transfer(address to, uint256 value) public returns (bool) {
        return _tranfer(msg.sender,to, value);
        
    }
    
    function _tranfer(address from, address to, uint256 value) internal returns (bool) {
        require(from != address(0),"ERC20:transfer from zero address");
        require(to != address(0),"ERC20:transfer to zero address" );
       
        _balances[from] = _balances[msg.sender]- value;
        _balances[to] = _balances[to]+ value;
        
        emit Transfer(from,to,value);
        
        return true;
        
    }
    
    function transferFrom(address owner, address to, uint256 value)public returns(bool) {
        require(_allowance[owner][msg.sender] >= value, "ERC20:not allowed to address");
        return _tranfer(owner,to,value);
    }
    
}
