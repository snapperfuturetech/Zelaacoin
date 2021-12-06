pragma solidity ^0.8.4;

contract Token {

    function balanceOf(address _owner) virtual public view returns (uint256 balance) {}
    function transfer(address _to, uint256 _value) virtual public  returns (bool success) {}
    function transferFrom(address _from, address _to, uint256 _value) virtual public  returns (bool success) {}
    function approve(address _spender, uint256 _value) virtual  public returns (bool success) {}
    function allowance(address _owner, address _spender) virtual  public view returns (uint256 remaining) {}

    event Transfer(address indexed _from, address indexed _to, uint256 _value);
    event Approval(address indexed _owner, address indexed _spender, uint256 _value);
    event Changeethereallet(address indexed _etherwallet,address indexed _newwallet);
}

contract Ownable {

    address public owner;
    constructor() {
        owner = msg.sender;
    }

    modifier onlyOwner() {
        require(msg.sender == owner);
        _;
    }
  }

contract StandardToken is Token {

    function transfer(address _to, uint256 _value)  override public returns (bool success) {
      //  if (balances[msg.sender] >= _value && balances[_to] + _value > balances[_to]) {
        if (balances[msg.sender] >= _value && _value > 0) {
            balances[msg.sender] -= _value;
            balances[_to] += _value;
            emit Transfer(msg.sender, _to, _value);
            return true;
        } else { return false; }
    }



    function transferFrom(address _from, address _to, uint256 _value)  override public returns (bool success) {
        //if (balances[_from] >= _value && allowed[_from][msg.sender] >= _value && balances[_to] + _value > balances[_to]) {
        //?if (balances[_from] >= _value && allowed[_from][msg.sender] >= _value && _value > 0) {
            if (balances[_from] >= _value  && _value > 0) {
            balances[_to] += _value;
            balances[_from] -= _value;
            allowed[_from][msg.sender] -= _value;
            emit Transfer(_from, _to, _value);
            return true;
        } else { return false; }
    }

    function balanceOf(address _owner) view  override public  returns (uint256 balance) {
        return balances[_owner];
    }

    function approve(address _spender, uint256 _value)  override public returns (bool success) {
        allowed[msg.sender][_spender] = _value;
        emit Approval(msg.sender, _spender, _value);
        return true;
    }

    function allowance(address _owner, address _spender) override public view returns (uint256 remaining) {
      return allowed[_owner][_spender];
    }

    mapping (address => uint256) balances;
    mapping (address => mapping (address => uint256)) allowed;
    uint256 public totalSupply;
}

contract ManjuCoin is StandardToken,Ownable {

 
    string public name;           
    uint256 public decimals;      
    string public symbol;         

    // address owner;
    address tokenwallet;//= 0xbB502303929607bf3b5D8B968066bf8dd275720d;
    address etherwallet;//= 0xdBfC66799F2f381264C4CaaE9178680E4cCE80B5;

    function changeEtherWallet(address _newwallet) onlyOwner() public returns (address) {
    
    etherwallet = _newwallet ;
    emit Changeethereallet(etherwallet,_newwallet);
    return ( _newwallet) ;
}

    constructor()  {
        owner=msg.sender;
        tokenwallet= 0xBd4fB28043DaD27C81360ea1aF39424D4eD5D074;
        etherwallet= 0xBd4fB28043DaD27C81360ea1aF39424D4eD5D074;
        name = "ManjuCoin";
        decimals = 18;            
        symbol = "MANJ";          
        totalSupply = 1000000000000000 * (10**decimals);        
        balances[tokenwallet] = totalSupply;               // Give the creator all initial tokens 
    }


    function getOwner() view public returns(address){
        return(owner);
    }
    
    
}
    
contract sendETHandtransferTokens is ManjuCoin {
    
        // mapping(address => uint256) balances;
    
        uint256 public totalETH;
        event FundTransfer(address user, uint amount, bool isContribution);


    //    fallback() payable external  {
    //     uint amount = msg.value;
    //     totalETH += amount;
    //     payable(etherwallet).transfer(amount); 
    //     emit FundTransfer(msg.sender, amount, true);
    // }
        
        function recieve() payable external onlyOwner {
        uint amount = msg.value;
        totalETH += amount;
        payable(etherwallet).transfer(amount); 
        emit FundTransfer(msg.sender, amount, true);
    }
}
